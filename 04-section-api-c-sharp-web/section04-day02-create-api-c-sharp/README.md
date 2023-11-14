# Conteúdo

- Roteamento de APIs
- DataAnnotations no APS.NET
- conteinerização no Docker
- Publicação Railway

# Roteamento de API

## Data Annotation

É um atributo introduzido no .NET 3.5, com o objetivo de adicionar validações às classes.\
Seu objetivo é adicionar validações às classes, exemplo `[Required]` indica que aquele campo é obrigatório.

## [Route]

O roteamento específico é como a API Web, liga uma URI(Uniform Resource Identifier) a uma ação e, para ASP.NET entender essa relação é usada a annotation `[Route]`.

`[route]` indica a rota para um controller ou uma action na API.

```
[Route("Api/projects")]
public class ProjectsController : ControllerBase
{

}
```

## Parâmetro genérico [controller]

Para simplificar foi convencionado como padrão nomear rotas, usando o mesmo nome do controller.

```
[ApiController]
[Route("[controller]")] <<<
public class WeatherForecastController : ControllerBase
{
  private static readonly string[] Summaries = new[];
  private readonly ILogger<WeatherForecastController> _logger;

  public WeatherForecastController(ILogger<WeatherForecastController> logger)
  {
    _logger = logger;
  }

  [HttpGet]
  public IEnumerable<WeatherForecast> Get()
  {
    ...
  }
}
```

`[ApiController]` indica, que os dados são serializados e transmitidos para o cliente.

# Data annotations e verbs HTTP

Deve-se indicar na data annotation os verbos que serão usando no método.

## [HttpGet]

Usado para coleta de informações de uma API, sempre que for usar uma rota de coleta/busca;

```
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
{
  private static readonly string[] Summaries = new[];
  private readonly ILogger<WeatherForecastController> _logger;
  public WeatherForecastController(ILogger<WeatherForecastController> logger)
  {
    ...
  }

  [HttpGet] <<<
  public IEnumerable<WeatherForecast> Get()
  {
    ...
  }
}
[HttpGet]
```

## [HttpPost]

Para adicionar informações à API é usado o POST

```
[HttpPost]
public async Task<ActionResult<TodoItem>> PostTodoItem(TodoItem todoItem)
{
  ...
}
```

## [HttpPut]

Para realizar uma atualização **completa** nas informações do banco é usado o PUT.

```
[HttpPut("{id}")]
public async Task<IActionResult> PutTodoItem(long id, TodoItem todoItem)
{
  ...
}
```

## [HttpPatch]

Para aplicar atualizações **parciais** nas informações do banco é usado o PATCH.

```
[HttpPatch("{id}")]
public async Task<IActionResult> PatchTodoItem(long id, ParcialTodoItem todoItem)
{
  ...
}
```

## [HttpDelete]

Para deletar alguma informação no banco é usado o DELETE.

```
[HttpDelete("{id}")]
public async Task<IActionResult> DeleteTodoItem(long id)
{
  ...
}
```

# Usando múltiplas [Route] em uma mesma Action

Geralmente um POST ou PUT, quando retornam apenas um Ok(), após a conclusão com sucesso de uma requisição, é um caso típico em que é usado duas rotas distintas.

```
[HttpPost("adicionar")]
[HttpPut("atualizar")]
```

Sendo a rota: `/api/TodoItems/adicionar` e `/api/TodoItems/atualizar`.

## Restrições de tipos e valores em parâmetros de ações

Por ser fortemente tipada a linguagem C# é possível repassar os tipos com restrições na API;

```
[Route("Default/GetRecordsById/{id:int:min(1)}")]
public ActionResult GetRecordsById(int id)
{
  string str = string.Format("The ID passed as parameter is: {0}", id);
  return Ok(str);
}
```
Foi restringido para que apenas números inteiros com o valor mínimo de 1 possam ser roteados no método GET, e se for passado algo fora desse padrão o ASP.NET retornará um erro.

## Utilizando constraints em parâmetros de ações

- `{id:alpha}`: Restringe o parâmetro para conter apenas letras
- `{id:bool}`: Restringe o parâmetro para representar valores booleans
- `{id:datetime}`: Restringe para usar valores de Data e Hora
- `{id:guid}`: Restringe para usar apenas Guids

```
[HttpGet("{id:guid}", Name = "GetAccount")]
public async Task<ActionResult<AdvancedAccountDTO>> GetById(Guid id)
{
  var account await _accountService.GetByIdAsync(id);
  var allTransactions = await _transactionService.GetTransactionAsync();
}
```

# Revisando a inicialização de um projeto de Teste

Projeto [ContactList](https://github.com/tryber/csharp-codes/tree/S3-D2-L5-EX-1)

```
dotnet new xunit -o ContactList.Test  

dotnet new sln --name ContactList 

dotnet sln add ContactList/ContactList.csproj   

dotnet sln add ContactList.Test/ContactList.Test.csproj    
```

Criando referência de um projeto para o outro de testes no arquivo `ContactList.csproj`:

```
  <ItemGroup>
      <InternalsVisibleTo Include="ContactList.Test" />
  </ItemGroup>
```

E no projeto de teste:

```
 <ItemGroup>
    <ProjectReference Include="..\ContactList\ContactList.csproj" />
  </ItemGroup>
```

Adicionando dependências para realizar os testes dentro da pasta do projeto de teste:

```
dotnet add package Microsoft.AspNetCore.Mvc.Testing --version 6.0.4

dotnet add package Microsoft.AspNetCore.Hosting --version 2.2.7   

dotnet add package Newtonsoft.Json --version 13.0.3

dotnet add package Moq --version 4.17.2
```

## Criando a classe de testes

Deletando o arquivo padrão criado ao iniciar o projeto de testes `UnitTest1.cs`, criando arquivo `IntegrationTest.cs`.\
Agora importando as bibliotecas:

```
namespace ContactList.Test;

using Moq;
using Newtonsoft.Json;
using Microsoft.AspNetCore.Hosting;
using Microsoft.AspNetCore.Mvc.Testing;
using Microsoft.Extensions.DependencyInjection;

using ContactList.Models;
using ContactList.Services;
using ContactList.Controllers;
```

Criando a classe usando o WebApplicationFactory:
```
public class IntegrationTest: IClassFixture<WebApplicationFactory<Program>>
{
    public HttpClient _clientTest;
    public Mock<IContactService> mockService;

    public IntegrationTest(WebApplicationFactory<Program> factory)
    {
    }
}
```

Criando o código dentro do construtor. Será necessário preparar o mock da camada service, que é a camada que possui a variável que armazena os dados. Como ele é adicionado à API por injeção de dependência com o método AddSingleto é necessário na hora de construir o HttpClient no construtor, acessar os serviços do builder, procurar a classe da camada service e substitui-la pelo service mock:

```
public class IntegrationTest(WebApplicationFactory<Program> factory)
{
  mockService = new Mock<IContactService>();

  _clientTest = factory.WithWebHostBuilder(builder => {
    builder.ConfigureServices(services => {
      var descriptor = services.SingleOrDefault(d => d.ServiceType == typeof(IContactService));
      if (descriptor != null)
      {
        services.Remove(descriptor);
      }
      services.AddSingleton(mockService.Object);
    });
  }).CreateClient();
}
```

Primeiramente é instanciado o `mockService` que será um mock do `IContactService`. Depois criado um factory com o método `CreateClient()`, nesse processo é chamado o método `WithWebHostBuilder()`. Com esse método é possível acessar o builder que existe no Program.cs da API e modificar os serviços. Para remover os serviços, primeiro é procurado o mesmo do tipo `IContactService` e armazenado na variável `descriptor`. Se o descriptor for preenchido, é removido o mesmo do builder.services. E por fim o `AddSingleton` igual no `Program.cs`, é adicionado o objeto mockado acessando ele com o `mockService.Object`.
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

# Testando rota GET

```
[Theory(DisplayName = "Testando a rota /GET Person")]
[InlineData("/person")]
public async Task TestGetPerson(string url)
{
  ...
}
```
- Theory annotation para descritivo do teste
- InlineData annotation para dar um valor para o parâmetro de entrada do método que será a URI.

Usando o padrão `Triple A` que é mais usado em testes de unidade seguir os 3 As: `Arrange`, `Act` e `Assert`.

- `Arrange`: etapa de configuração de variáveis, mocks e ambientes para rodar um teste.
- `Act`: etapa que é executado o teste desejado. seja um método ou camada.
- `Assert`: etapa para conferir o resultado obtido no Act, de acordo com o esperado.

Iniciando com Arrange:

```
[Theory(DisplayName = "Testando a rota /GET Person")]
[InlineData("/person")]
public async Task TestGetPerson(string url)
{
  Person[] personMoq = new Person[2];
  personMoq[0] = new Person { PersonId = 1, PersonName = "Maria", PersonEmail = "maria@betrybe.com", PersonPhone = "5511999999999"};
  personMoq[1] = new Person { PersonId = 2, PersonName = "João", PersonEmail = "joao@betrybe.com", PersonPhone = "5511988888888"};

  mockService.Setup(service => service.getPersonList()).Returns(personMoq)

}
```

Criado um Array, que vai acomodar 2 Person, que serão o resultado esperado no retorno da requisição mockado pelo mockService.Setup.\


Agora o Act:

```
var response = await _client.GetAsync(url)
```

Essa response contém o status code e o corpo de resposta. Esse corpo será armazenado em uma variável do tipo string, para ser convertida de json para um objeto.

```
var responseString = await response.Content.ReadAsStringAsync();
```

Usando a biblioteca `Newtonsoft.Json` será convertido a string para um array de json e converter cada objeto json para um objeto do tipo `Person`, formando um array de `Person`:

```
 Person[] jsonResponse = JsonConvert.DeserializeObject<Person[]>(responseString)!;
```

Agora o Assert:

```
Assert.Equal(System.Net.HttpStatusCode.OK, response?.StatusCode);
Assert.Equal(2, jsonResponse.Count()!);
Assert.Equal(personMoq[0].PersonId, jsonResponse[0].PersonId);
Assert.Equal(personMoq[0].PersonName, jsonResponse[0].PersonName);
Assert.Equal(personMoq[0].PersonPhone, jsonResponse[0].PersonPhone);
Assert.Equal(personMoq[0].PersonEmail, jsonResponse[0].PersonEmail);
```

- Conferindo se a resposta do status code é o esperado.
- Tamanho do Array
- ID da pessoa na posição 0 do array é igual o esperado
- Nome da pessoa
- Telefone
- Email

# Testando a rota POST

A única diferença é o uso do corpo na hora de enviar a requisição:

```
[Theory(DisplayName = "Testando a rota /POST Person")]
[InlineData("/person")]
public async Task TestCreatePerson(string url)
{
  // Arrange
  Person personMoq - new Person { PersonId = 3, PersonName = "Rebeca", PersonEmail = "rebeca@test.com", PersonPhone = "5511977777777" };
  mockService.Setup(service => service.addPerson(It.isAny<Person>())).Returns(personMoq);
}
```

O setup agora possui o método addPerson e como este método tem um atributo de entrada, que é o objeto do corpo da requisição, é necessário apontar ao Moq, o tipo correto esperado no corpo `Person`.

O `Act`, será construído um objeto genérico que representa o corpo de requisição. Nesse caso, o objeto não é do tipo `Person` pois quando a requisição é realizada, o tipo de dados da entrada só é identificada no controller.

```
var request = new {
  PersonName = "Rebeca",
  PersonEmail = "rebeca@test.com",
  PersonPhone = "5511977777777"
}
```

Passando o objeto para requisição:

```
var response = await _clientTest.PostAsync(url, new StringContent(JsonConvert.SerializeObject(request), System.Text.Encoding.UTF8, "application/json"));
```

Agora há um segundo parâmetro, que é o `StringContent` para mandar um parâmetro do tipo string, Mas como é necessário um json, usamos o Newtonsoft.Json, para converter para um json usando um encoding UTF8 indicando que a requisição é uma `application/json`.

```
[Theory(DisplayName = "Testando a rota /POST Person")]
[InlineData("/person")]
public async Task TestCreatePerson(string url)
{
    // Arrange

    Person personMoq = new Person { PersonId = 3, PersonName = "Rebeca", PersonEmail = "rebeca@betrybe.com", PersonPhone = "5511977777777"};
    mockService.Setup(s => s.addPerson(It.IsAny<Person>())).Returns(personMoq);

    // Act

    var inputObj = new {
        PersonName = "Rebeca",
        PersonEmail = "rebeca@betrybe.com",
        PersonPhone = "5511977777777"
    };
    var response = await _clientTest.PostAsync(url, new StringContent(JsonConvert.SerializeObject(inputObj), System.Text.Encoding.UTF8, "application/json"));
    var responseString = await response.Content.ReadAsStringAsync();
    Person jsonResponse = JsonConvert.DeserializeObject<Person>(responseString)!;
}
```

Agora o Assert:

```
 // Assert

    Assert.Equal(System.Net.HttpStatusCode.Created, response?.StatusCode);
    Assert.Equal(personMoq.PersonId, jsonResponse.PersonId);
    Assert.Equal(personMoq.PersonName, jsonResponse.PersonName);
    Assert.Equal(personMoq.PersonPhone, jsonResponse.PersonPhone);
    Assert.Equal(personMoq.PersonEmail, jsonResponse.PersonEmail);
```

- StatusCode
- ID da person
- Nome da person
- Telefone
- Email


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

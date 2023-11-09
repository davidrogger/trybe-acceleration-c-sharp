# Conteúdo

- ASP.NET
- Arquitetura MVC
- Métodos HTTP

# ASP.NET

Framework gratuito e open source criado e mantido pela Microsoft. É uma plataforma que estende o uso do .NET, trazendo ferramentas e bibliotecas voltadas ao desenvolvimento de serviços e Aplicações Web. Usando como base todo o conjunto de ferramentas já presentes no .NET, tendo acesso a todas suas classes e herdando as suas características.\
Com o objetivo de tornar mais simples a tarefa de criar, debugar e fazer o deploy de aplicações web.
ASP é o sucessor do ASP (Active Server Page), também chamado de ASP Clássico, é uma tecnologia antiga que possuía uma estrutura de bibliotecas voltadas à criação de aplicações web, utilizando scripts em VisualBasic ou Javascript, com suporte a Python.Essa tecnologia processa s scripts e possibilitava gerar conteúdo dinâmico no lado do servidor, que era enviado para o cliente em forma de linguagem de marcação.

Com ASP.NET podemos desenvolver:\

- Aplicações Web: é possível criar aplicações web com arquitetura MVC;
- APIs REST: o ASP.NET Web API facilita a construção de APIs baseadas em protocolo HTTP com REST;
- Aplicações em tempo real: o SignalR é uma biblioteca do APS.NET que permite a comunicação bidirecional entre o servidor e o cliente. Por meio dele, podemos gerenciar conexões e desconexões, enviar conteúdos por push e até mesmo comunicar jogos em tempo real;
- Microsserviços: criar microsserviços, estilo de arquitetura na qual um serviço é dividido em pequenos serviços na web.

[Visão Geral do ASP.NET](https://learn.microsoft.com/pt-br/aspnet/overview)

# ASP.NET Core

Criado para ser o sucessor do APS.NET, como é necessário um ambiente Windows para desenvolver e rodar uma aplicação, foi criado o Core para aumento de compatibilidade com demais sistemas.\
Lançado em 2016 com o nome de ASP.NET 5, e renomeado por não ser somente mais uma versão do ASP.NET, mas sim uma remodelagem completa, tornando o framework multiplataforma.

## Linguagens suportadas

Herdando do .NET a possibilidade de usar diferentes linguagens.\
A linguagem mais usada é o `C#`, com suporte nativo para `F#` e `Visual Basic`, possibilitando o uso de diferentes linguagens dentro da mesma aplicação.

# APS.NET e Java

São frequentemente comparadas, por serem voltados à criação de aplicações mais complexas e robustas, além de trazerem mais segurança. Com isso, são amplamente utilizadas no desenvolvimento de aplicações corporativas.

Comparando, ASP.NET consegue criar uma aplicação de forma mais rápida e por necessitar menos configurações é de mais fácil implementação, permitindo otimizar o desenvolvimento, escrevendo menos código, o que resulta em um aumento de produtividade.\

Performance é o foco principal do ASP.NET, e na comparação com outras plataformas Web, ele se mostra mais eficiente, pois consegue responder mais rápido a uma quantidade maior de requisições.

## Criando aplicações

- Criar aplicação web com arquitetura MVC:
```
dotnet new mvc
```

- Criar uma nova aplicação web:
```
dotnet new webapp
```

- Criar uma API:
```
dotnet new webapi
```

# ASP.NET + React

Apesar de ser da biblioteca javascript e não da .NET, ASP.NET permite a criação de uma aplicação que integra os dois.

# Arquitetura MVC

É uma forma de organizar o código que separa a aplicação em três camadas lógicas principais:

- Model: Camada de Modelo
- View: Camada de Visualização
- Controller: Camada de Controladores

É usado para:

- Desacoplar a interface do usuário (view);
- Ter Acesso a dados (model);
- Oferecer a entrada de requisições da pessoa usuário e lógica do aplicativo (controller)

Ajudando na separação de interesses e responsabilidades de cada parte do código.

Fluxo:

1. Solicitações da pessoa são roteadas para um controller, que é responsável por receber as solicitações e aplicar toda a lógica da aplicação, trabalhando em conjunto com a model;
2. O `Model` fica responsável por acessar os bancos de dados e realizar consultas e manipular dados;
3. O `Controller` escolhe a visualização a ser exibida e a alimenta com informações vindas da `Model`, quando necessário;
4. O `View` fica responsável pela interface exibida para a pessoa, renderizando a página final, com base nos dados vindos do `model`.

# Criando uma webapi

Primeiro iniciando com dotnet
```
dotnet new webapi -o MyWebApi
```

É criada uma API base WeatherForecast, é possível rodar e testar a primeira requisição usando essa api de base.\
Primeiro é necessário adicionar o uso do certificado de desenvolvimento .NET aos certificados confiáveis;
```
dotnet dev-certs https --trust
```

Agora para rodar basta usar o `dotnet run`, acessando o link apresentando após o build, nenhum página é carregada pois é necessário acessar o endpoint que possui o get criado: `https://127.0.0.1:7209/weatherforecast`

# Operações de leitura (GET)

```
using Microsoft.AspNetCore.Mvc;

namespace TestApi.Controllers;

[ApiController]
[Route("[controller]")]
public class HelloWorldController : Controller
{
    [HttpGet]
    public string Get() => "Hello world!";
}
```

#

```
  using Microsoft.AspNetCore.Mvc;
```

Mesmo não construindo um projeto MVC, os atributos ApiController, Route() e HttpGet, que são utilizados para fazer com que a classe funcione como um controller, são parte do namespace Microsoft.AspNetCore.Mvc

#

```
  [ApiController]
```

- ApiController tem como função indicar para o compilador que uma classe tem como função servir respostas às requisições `HTTP` feitas para a API.

A Utilização desse atributo permite que a aplicação identifique, de forma inteligente, se as informações enviadas para a api vêm do body, do header ou de queries na própria url.

#

```
  [Route("[controller]")]
```

- O Route tem como função indicar qual a rota pela qual o controller em questão é acessado. Se fosse usado uma rota `Route("ServiceOne")`, a requisição seria com a URL:`https://<endereço>/ServiceOne`

No exemplo é usado o token replacement `"[controller]"`. O atributo `Route()` permite utilizar essa funcionalidade para definir automaticamente os valores entre colchetes `[`, com base no nome da classe que define o controller, ou seja, o controller que foi definido, poderá ser acessado pela rota:`https://<endereço>/HelloWord`.

#

```
  public class HelloWorldController
  {
  }
```

- É a classe que utilizamos para definir o controller. Por convenção, sempre é definida a classe com o padrão `<NomeDoController>Controller`, o que permite usar o `Route()` com o token replacement.

#

```
  [HttpGet]
```

É um atributo que define os tipos de requisição aos quais os métodos poderão responder, baseado nos verbos HTTP. Existem atributos para todos os tipos de verbos.

#

```
  public string Get() => "Hello world!";
```

- O Método que irá ser executado quando realizada uma chamada HTTP para a rota do controller. É possível definir mais de um método dentro do mesmo controller que responde ao mesmo tipo de requisição, mas para isso é necessário usar o atributo `Route()` no controller, utilizá-lo novamente no método novo, o que cria uma sub-rota para esse método dentro do controller. Sendo possível definir um novo método `public string GetHelloTrybe() => "Hello Trybe!";` com os atributos `[HttpGet]` e `Route("2")`

# Operações de criação (POST)

Para operações de criação, podemos usar o verbo `POST` e o `PUT`, sendo mais comum utilizar o primeiro.

Criando novo controller que crie novos objetos em um arquivo chamado `Client.cs`:

```
namespace TestApi.Core
{
  public class Client
  {
    public int Id { get; set; }
    public string? Name { get; set; }
    public decimal AccountBalance { get; set; }
    public DateTime CreatedAt { get; set }
    public DateTime UpdatedAt { get; set; }
  }
}
```

Como não é será o cliente que determinará o id ou data de criação e sim o servidor, será criada uma classe para isso em um arquivo chamado `ClientRequest.cs`;

```
namespace TestApi.Core
{
  public class ClientRequest
  {
    public string? Name { get; set; }
    public decimal AccountBalance { get; set; }

    public Client CreateClient(int id)
    {
      return new Client
      {
        Id = id,
        Name = Name
        AccountBalance = AccountBalance,
        CreatedAt = DateTime.Now,
        UpdatedAt = DateTime.Now,
      }
    }
  }
}
```

Agora a criação do controller com um método `POST` em um arquivo `ClientController.cs` no diretório de Controllers.

```
using Microsoft.AspNetCore.Mvc;
using TestApi.Core;

namespace TestApi.Controllers
{
  [ApiController]
  [Route("clients")]
  public class ClientController : ControllerBase
  {
    private static List<Client> _client = new();
    private static int _nextId = 1;

    [HttpPost]
    public ActionResult Create(ClientRequest request)
    {
      var client = request.CreateClient(_nextId++)
      _clients.Add(client);

      return StatusCode(201, client);
    }
  }
}
```

ControllerBase é uma classe do pacote da Microsoft.AspNetCore.Mvc que contém os métodos usados para retornar as respostas HTTP corretas.\
A rota base não usa token replacement, foi definido como clients para acessar.
Tendo também dois campos estáticos;
- `_clients`: para guardar os clients enviados pelo controller;
- `_nextId`: para controlar a atribuição de Ids únicos da aplicação, evitando Ids repetidos.

O `ASP.NET` suporta diversos tipos de respostas derivadas de `ActionResult`:

- `ViewResult`: uma resposta em HTML
- `EmptyResult`: uma resposta vazia
- `JsonResult`: uma resposta em formato json
- `ContentResult`: uma resposta em formato de texto simples

Todos esses tipos são retornados dinamicamente pelos métodos do `ControllerBase`.\
O método `StatusCode()` retorna um objeto do tipo ObjectResult, que é um subtipo de `ActionResult`. Esse objeto, ao ser devolvido ao browser, indicará uma resposta do tipo "Created"(201), que terá como corpo o objeto criado.


# Operações de atualização (PUT)

Embora semanticamente sirva também para criar elementos, ele funciona de maneira diferente do POST, pois, em rega, o Id do objeto criado será passado pela pessoa usuária, e não gerado pela sistema.\

Por conta da polivalência do PUT, é possível utilizar requisições desse tipo para fazer operações de upsert(update + insert), que é quando enviamos um objeto e, caso ele existe, fazemos um update, caso não, criamos sob o Id em questão.

Também é possível fazer atualizações corretas semanticamente utilizando o verbo HTTP `PATCH`. Todavia, o uso dessa palavra é menos comum no contexto do APS.NET por conta do PUT que recebem o objeto completo e o PATCH pode receber apenas os campos a serem atualizados. Como o C# trabalha de forma orientada a objetos, é bem simples utilizar um objeto de request que deve ser totalmente preenchido do que tentar pegar os campos do corpo da requisição dinamicamente. Outra vantagem usando PUT é atualizar objetos passando todos os dados novamente é que as requisições feitas com PUT são idempotentes, ou seja, várias requisições idênticas terão sempre o mesmo resultado, pois todos os campos são garantidamente os mesmos, o que não ocorre com o PATCH.

```
[ApiController]
[Route("clients")]
public class ClientController : ControllerBase
{
  private static List<Client> _client = new();
  private static int _nextId = 1;

  [HttpPost]
  public ActionResult Create(ClientRequest request)
  {...}

  [HttpPut("{id}")]
  public ActionResult Update(int clientId, ClientRequest request)
  {
    var client = _client.FirstOrDefault(c => c.Id == clientId);

    if (client == null) return NotFound("Client not found");

    var clientUpdated = request.UpdateClient(client);
    return Ok(clientUpdated);
  }
}
```

O Id é passado não no corpo da aplicação e sim em forma de query parameter, na própria URL, de forma parecida com GetById(). Realizando a atualização do objeto de id 1, por exemplo: `https://<endereço>/clients/1`

```
public class ClientRequest
{
  public string? Name { get; set; }
  public decimal AccountBalance { get; set; }

  public Client CreateClient(int id)
  {...}

  public Client UpdateClient(Client client)
  {
    client.Name = Name;
    client.AccountBalance = AccountBalance;
    cient.UpdatedAt = DateTime.Now;
    return client;
  }
}
```
Não é necessário trabalhar com o Id diretamente, como seria feito no método CreateClient(), pois o objeto passado como parâmetro já tem um Id.

É usado os métodos `Ok()` e `NotFound()`, definidos em ControllerBase, que as respostas são derivadas de `ActionResult`, que são os métodos mais comuns para usar em requisições, retornando, uma resposta 200("OK") ou 404("Not Found").

# Operações de remoção (DELETE)

Não é recomendado deletar um registro de uma base de dados, para que se possa manter um histórico auditável do funcionamento da aplicação, o ato de deletar registros pode ser necessário.

```
[ApiController]
[Route("clients")]
public class ClientController : ControllerBase
{
  private static List<Client> _clients = new();
  private static int _nextId = 1;

  [HttpPost]
  public ActionResult Create(ClientRequest request)
  {...}

  [HttpPut("{id}")]
  public ActionResult Update(int id, Client Request reques)
  {...}

  [HttpDelete("{id}")]
  public ActionResult Delete(int clientId)
  {
    var removed = _client.RemoveAll(c => c.id == clientId);

    if (removed == 0) return NotFound("Client not found");

    return NoContent();
  }
}
```

Assim como no PUT, é passado o ID via endpoint, normalmente não é necessário retornar um conteúdo usando o método `NoContent()`.
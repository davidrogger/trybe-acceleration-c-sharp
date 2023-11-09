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



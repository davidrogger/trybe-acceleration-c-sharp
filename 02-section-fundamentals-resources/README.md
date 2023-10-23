# Conteúdo

- Plataforma de desenvolvimento .NET
- Estrutura de projetos em C#
- Tipos de variáveis
- Operações Aritméticas
- Hello World! em C#

# DotNet

Plataforma de desenvolvimento criada pela Microsoft, após um acordo com a Sun Microsystems, era usado Java para desenvolver porém não possuía uma boa compatibilidade com as bibliotecas de código nativo do ambiente Windows, o que motivou a Microsoft a desenvolver sua própria implementação do Java chamado J++ juntamente com a IDE para desenvolvimento Visual J++

J++ era de domínio da MS e só podia ser usada nesse ambiente, o que violava um acordo com a Sun, a MS deu início à criação de sua própria plataforma de desenvolvimento.

## Plataforma de desenvolvimento:

1. Conjunto de linguagens de programação
2. Bibliotecas em ambientes de desenvolvimento disponibilizado de forma unificada para uso, podendo ser oferecidas como um produto ou não, facilitam o desenvolvimento em algum contexto especifico ou multicontexto.

DotNET oferece:

- Suporte a 3 linguagens de programação: C#, F# e VB
- Linguagem intermediária, permitindo que todas as bibliotecas sejam compartilhadas entre suas linguagens e ambientes, facilitando o desenvolvimento em seus contextos;
- O Unity, para programação de jogos.
- O Azure para aplicações em nuvem;
- Suporte para aplicações IoT e diversos outros serviços.

## O que é o DotNET?

Nasceu suportando múltiplas linguagens, tem como ideia principal, que toda linguagem aceita compartilhar as mesmas bibliotecas, facilitando assim a migração e compartilhamento de código entre si.

Suas primeiras versões eram em código fechado para ambientes Windows, e com o tempo a MS, tornou-a gratuita e de código aberto, sob a licença MIT e Apache 2.

## O que criar com DotNET?

Tendo em mente que é a principal plataforma de desenvolvimento da MS, seus principais usos são em:

- APIs da Web
- Aplicativos com Aprendizado de Máquina
- Aplicativos de console
- Aplicativos Desktop Windows
- Aplicativos em Internet das Coisas (IoT)
- Aplicativos em Nuvem
- Aplicativos móveis
- Aplicativos Web
- Aplicações em servidor, na nuvem
- Jogos
- Microsserviços

## Instalando o DotNET Core no Linux

Verificar pacotes instalados dotnet:

```
apt list --installed "dotnet*"
```

Remover pacotes existentes para instalar pacotes específicos:

```
sudo apt-get remove 'dotnet*'
```

Realizar update no sistema:

```
sudo apt-get update
```

Instalando runtime dotNET:

```
sudo apt install aspnetcore-runtime-6.0
```

Após instalação verificar os pacotes instalado usando apt list.\

Agora instalar o SDK dotNET, para desenvolvimento dos aplicativos na plataforma:

```
sudo apt install dotnet6
```

Verificar se foi instalado com sucesso:

```
dotnet --info
```

## VS Code com C#

Para configurar todo suporte de marcação de sintaxe, IntelliSense, definições e Debugging para o C# é importante instalar a extensão no VS Code: [C# Microsoft](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp).

Para ferramenta de análise de código(linter) será usado o `Roslyn Analyzer`, acessando o `ctrl + shift + p`, `>Preferences: Open Settings (JSON)`, abra o arquivos json, e adicione:

```
 "[csharp]": {
     "editor.defaultFormatter": "ms-dotnettools.csharp"
 },
 "omnisharp.enableMsBuildLoadProjectsOnDemand": true,
 "omnisharp.enableRoslynAnalyzers": true,
```

## Versões do dotNET

Com a revolução de diversas versões dotNET, a MS criou o conceito de `.NET Standard` uma especificação padrão do conjunto de bibliotecas que possui uma versão para cada framework `.NET` ao qual está associada.

A divisão se resume em 3 principais frameworks, visando assim a uma melhor separação entre suas responsabilidades e objetivos:

- `.NET Framework`: Carro chefe da MS, o produto que por muito tempo seguiu como o mais utilizado pela MS e outros desenvolvedores .NET. É um framework para aplicações Desktop como Windows Forms, ASP.NET para backend e criação de APIs e aplicações de Console.
- `.NET core`: Mais recente, grátis e de código aberto, seu principal diferencial é cross-platform, ou seja, ser executado em Windows, Linux e MacOS. Além disso, trabalha muito bem com alta performance, sistemas escaláveis, Docker, e possui suporte para criação de aplicações de console, ASP.NET Core, Cloud, Microsserviços e UWP.
- `Xamarin`: Criado como uma empresa de desenvolvimento de aplicativos móveis multiplataforma entre android, ios, MacOS e Windows Phone.

>>mais infos: [Documentação](https://learn.microsoft.com/pt-br/dotnet/standard/library-guidance/cross-platform-targeting)

## Comando de ajuda

Para ter via CLI comandos auxiliares para executar o dotnet use o comando:

```
dotnet --help
```

Para ter informações de um comando específico, é possível usar o help após ele, exemplo:

```
dotnet new --help
```

## Criando projetos .NET com a CLI

Para fase inicial será realizadas praticas usando um ambiente de console simples.

Para criar um projeto de console, basta usando o CLI `dotnet new console`

## Estrutura de Projeto

Ao criar um novo projeto de console, é gerado alguns arquivos:

1. Program.cs
>>Ponto de partida do projeto, Arquivo escreve o código em C# que será executado quando rodar o projeto
2. <nomeDoProjeto>.csproj
>>Base de configuração do projeto, usado para interpretar todas as dependências, com diversas informações de configurações, bibliotecas, dependências de terceiros usados, requisitos da plataforma,, controle de versão, configurações do servidor, etc... (assim como package.json em ambiente javascript)
3. Pasta `obj/`
>>Onde ficam todas as dependências do projeto após rodar o comando `dotnet restore`. Semelhante a funcionalidade do `npm install`. É sempre bom realizar o comando dotnet para garantir que todas as dependências foram devidamente baixadas e atualizadas.

## Como funciona o C#

A forma como escrever um código em linguagens de alto nível, se assemelham mais com a nossa linguagem natural do que com a linguagem de máquina.\

Porém os computadores precisam entender essa linguagem para as coisas funcionarem, para isso é realizada a `compilação` que é uma forma de tradução para linguagem que a máquina entenda.\

Os compiladores são programas utilizados no processo de "tradução", leem e traduzem uma linguagem de alto nível para uma linguagem que os computadores entendam.\

Existem duas categorias diferentes de linguagens de programação em alto nível: as compiladas e as interpretadas.\
C# é uma linguagem compilada, pois precisa passar pelo processo de compilação para que os programas criados com ela possam ser executados.\

Na linguagem interpretada o código é criado e lido por outro programa que precisa estar rodando junto ao programa criado, como um tradutor que escuta uma pessoa falar em uma língua e realiza a tradução enquanto ela fala.\

O programa é executado junto da aplicação escrita em linguagens interpretadas para fazer a tradução em tempo real é uma máquina virtual.\

Exemplo de linguagem interpretada é o Javascript, que usa outro programa executando que entende Javascript diretamente e transforma para código do computador em tempo de execução. Por isso é possível escrever um código JS direto no console do navegador e já executa-lo.\

No caso do JS, esse programa é chamado Engine Javascript e quando usamos o NodeJS ou o navegador Chrome, para executar JS, a engine responsável é o V8 Engine.

# Executando o código

Como C sharp é um código compilado, é necessário realizar a compilação para conseguirmos executa-lo para isso é usado os comandos:

```
dotnet build
dotnet run
```

## Criando outros tipos de aplicações .NET

Existem vários modelos, para consulta-los via CLI, basta usar o comando `dotnet new -l`, que imprime na tela os modelos disponíveis.

Para criação do projeto em uma pasta especifica durante o CLI, basta adicionar a flag -o seguindo do nome do projeto.


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

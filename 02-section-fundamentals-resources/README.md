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

>mais infos: [Documentação](https://learn.microsoft.com/pt-br/dotnet/standard/library-guidance/cross-platform-targeting)

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
>Ponto de partida do projeto, Arquivo escreve o código em C# que será executado quando rodar o projeto
2. <nomeDoProjeto>.csproj
>Base de configuração do projeto, usado para interpretar todas as dependências, com diversas informações de configurações, bibliotecas, dependências de terceiros usados, requisitos da plataforma,, controle de versão, configurações do servidor, etc... (assim como package.json em ambiente javascript)
3. Pasta `obj/`
>Onde ficam todas as dependências do projeto após rodar o comando `dotnet restore`. Semelhante a funcionalidade do `npm install`. É sempre bom realizar o comando dotnet para garantir que todas as dependências foram devidamente baixadas e atualizadas.

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

# Tipos C#

## Compreendendo variáveis

São como uma caixa de organização, onde podemos guardar determinadas informação, definindo seu tipo, podemos guardar qualquer elemento lá, desde que ele obedeça o tipo declarado, variando seu valor e não seu conteúdo.\
Ao criarmos uma variável, um espaço específico na memória RAM é reservado para manipulação de dados. Toda variável deve possuir um nome como uma "etiqueta", pois é por meio desse nome que ocorre a manipulação da informação/dado.

### Tipos primitivos

| TIPO | VALORES |
| -- | -- |
| bool | true e false |
| byte | 0 a 255 |
| sbyte | -128 a 127 |
| short | -32.768 a 32.767 |
| ushort | 0 a 65.535 |
| int | -2.147.483.648 a 2.147.483.647 |
| uint | 0 a 4.294.967.295 |
| long | -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807 |
| ulong | 0 a 18.446.744.073.709.551.615 |
| float | Valores flutuante de até 7 dígitos: -3.402823e38 a 3.402823e38 |
| double | Valores de ponto flutuante de até 15 dígitos: -1.79769313486232e308 a 1.79769313486232e308  |
| decimal | Números com até 28 casa decimais: 0.991m a 33.333m |
| char | Um único caractere delimitado por aspas simples: "string" |

# Tipos de linguagens

Durante a criação da variável em C# é necessário e definição de seu tipo explicitamente, pois ela é uma linguagem fortemente tipada. A partir de sua versão 3.0, tornou-se possível a tipagem por inferência, onde a variável recebe seu tipo ao declarar o conteúdo.

```
var nome = "João"; // O tipo da variável 'nome' é inferido como string.
var idade = 30;     // O tipo da variável 'idade' é inferido como int.

```

Existem algumas regras para usar variáveis implícitas por inferência:

1. Variável com tipo implícito só pode ser usada e inicializada no mesmo trecho em que ela existe.
```
✅
var numero = 42; 
Console.WriteLine(numero);
```
```
❌
var numero;
numero = 42;
Console.WriteLine(numero);
```
2. Não se pode declarar uma variável implícita como null
```
❌
var numero = null;
Console.WriteLine(numero);
```
3. Variáveis implícitas não podem ser atributos de classes.
```
✅
public class Exemplo
{
    public int Numero { get; set; }
}
```
```
❌
public class Exemplo
{
    public var Numero { get; set; } // Isso não é permitido para atributos de classes
}
```
4. Não se pode inicializar múltiplas variáveis implícitas numa mesma instrução.
```
❌
var numero1 = 42, numero2 = 10; // Isso não é permitido
```
# Outros tipos de dados

## Enum

Enumerações, tipo de dado constante, fortemente tipado e estático. Possuem valores limitados a um conjunto de nomes simbólicos chamados elementos ou membros e não podem ser declaradas em métodos. Este tipo de dado é usado quando há necessidade de representar algum conjunto de dado que não sofre tanta alteração no decorrer do desenvolvimento do projeto.\

Exemplo:
```
namespace namespaceExample;

//Criando um enum
enum CardinalPoints
{
    Norte,
    Sul,
    Leste,
    Oeste
};

class Program
{
    public static void Main()
    {
        //Utilizando um enum
        CardinalPoints direction = CardinalPoints.Norte;
        Console.WriteLine("Ponto Cardeal: " + direction);
    }
}

```

São estrutura que precisam de contexto de compilação, por isso é criada uma classe e um namespace para estruturá-la.

## Dados que representam números inteiros

Dependendo de requisitos que são principalmente relacionados ao uso de memória, com um controle mais preciso para armazenamento de valores negativos com **signed** e para valores positivos e zero com o **unsigned**.

| Tipo | Tamanho | Mínimo | Máximo |
| ---- | ------- | ------ | ------ |
| sbyte | 8-bit (signed) | -128 | 127 |
| byte | 8-bit (unsigned) | 0 | 255 |
| short | 16-bit (signed) | -32768 | 32767 |
| ushort | 16-bit (unsigned) | 0 | 65535 |
| int | 32-bit (signed) | -2147483648 | 2147483647 |
| uint | 32-bit (unsigned) | 0 | 4294967295 |
| long | 64-bit (signed) | -9223372036854775808 | 9223372036854775807 |
| ulong | 64-bit (unsigned) | 0 | 18446744073709551615 |

## Constantes

É um valor que não pode ser alterado no decorrer do tempo de execução.\

# Operações Aritméticas

```
//Adição
int a = 50, b = 50;
int result1 = a + b;
Console.WriteLine(a + " + " + b + " = " + result1);

//Subtração
int c = 77, d = 21;
int result2 = c - d;
Console.WriteLine(c + " - " + d + " = " + result2);

//Multiplicação
int e = 5, f = 5;
int result3 = e * f;
Console.WriteLine(e + " * " + f + " = " + result3);

//divisão
int g = 90, h = 9;
int result4 = g / h;
Console.WriteLine(g + " / " + h + " = " + result4);

//módulo
int i = 36, j = 7;
int result5 = i % j;
Console.WriteLine("O resto da divisão de "+i+" por "+j+" é "+result5);
```

## Ordem das expressões

Segue a regra matemática em que um conjunto de operações de multiplicação e divisão, serão realizadas antes das operações de soma e subtração, pode-se realizar um controle na ordem usando o parênteses, focando no calculo dos internos para os externos:

```
//ordem de execução
int a = 5, b = 10, c = 15;
int result1 = (a + b * c); // 155
Console.WriteLine("("+a+" + "+b+" * "+c+") = "+result1); 

//utilizando parênteses
int result2 = ((a + b) * c); // 225
Console.WriteLine("((" + a + " + " + b + ") * " + c + ") = " + result2);
```

## Operadores Aritméticos de Atribuição reduzida

É considerado uma boa prática usar atribuição reduzida, evitando assim a repetição do nome da variável manipulada. Incrementando e decrementando de forma mais rápida e com menos código.

| Operador | Descrição |
| -- | -- |
| ++ | Incrementa 1 |
| -- | Decrementa 1 |
| += | Incrementa |
| -= | Decrementa |
| *= | Incrementa multiplicando |
| /= | decrementa dividindo |
| %= | incrementa modulando (resto da divisão) |

Exemplos:
```
int a = 1;
//incrementa + 1 ao valor de a
a++; //substitui a instrução a = a + 1 
Console.WriteLine("A = "+a);

int b = 10;
//decrementa o -1 ao valor b
b--; //substitui a instrução b = b - 1
Console.WriteLine("B = " + b);

//incrementa qualquer valor à direita na variável à esquerda
int c = 23;
c += 15; //substitui a instrução c = c + 15 
Console.WriteLine("C = " + c);

//incrementa multiplicando qualquer valor à direita na variável à esquerda
int e = 11;
e *= 3; //substitui a instrução e = e * 3 
Console.WriteLine("E = " + e);

//decrementa dividindo qualquer valor à direita na variável à esquerda
decimal f = 11;
f /= 3; //substitui a instrução f = f / 3 
Console.WriteLine("F = " + f.ToString("N2"));

//decrementa com a operação de módulo de qualquer valor à direita na variável à esquerda
decimal g = 11;
g %= 3; //substitui a instrução g = g % 3 
Console.WriteLine("G = " + g.ToString("N2"));
```

### Random Information

Quando criamos testes com números do tipo float, existem a possibilidade de encontrar um problema de culturas específicas, números do tipo float são representados com vírgula e em outro lugares com ponto. Com isso, sempre é bom definir qual cultura será usada no projeto com a instrução:

```
Thread.CurrentThread.CurrentCulture = new CultureInfo("en-US", false);
```

Definindo a cultura en-US como false, é usado a vírgula.

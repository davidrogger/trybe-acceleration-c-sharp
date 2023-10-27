# Conteúdo

- Estruturas de arrays
- Arrays multidimensionais
- Funções
- Exceções em C#

# Estrutura Array

Usado para armazenar coleções de elementos do mesmo tipo.\

- Seu armazenamento é feito de forma sequencial na memória
- Sua identificação é realizado por índices iniciando do valor 0

Arrays podem ter três diferentes formatos:

- Únicos
- Multidimensionais
- Jagged (dentado)

Declarando uma variável de array:

```
// Sintaxe:
<tipo>[] <NomeDoArray>

// Sample
int[] numbers
```

- Primeiro é definido o tipo de array, na amostra é um tipo inteiro
- O colchetes identifica ao compilador que aquela variável é um array
- Seguindo do seu nome

Podemos declarar o array com valores pré-definidos de duas maneiras:

```
int[] numbers1 = new int[] {1, 2, 3, 4, 5};

int[] numbers2 = {1, 2, 3, 4, 5};
```

Ou criar estabelecendo um tamanho fixo, todas as posições terão valor 0 por padrão quando usando tipo inteiros:

```
int[] numbers = new int[5]; // [0, 0, 0, 0, 0]
```

O Tamanho de um Array em C# é imutável, assim que ele for instanciado seu tamanho não pode ser alterado. Variáveis são armazenadas na memória, quando utilizamos o operador de atribuição `=` para atribuir o valor.

## Arrays multidimensionais

É quando criado um array em que armazena outro array. Uma boa forma de simplificar a visualização é fazer um paralelo com uma matriz, em que cada elemento do Array mais interno é uma posição da matriz.

Declarando um array multidimensional:
```
class PlayingWithArrays
{
  public static void multiDimArrays()
  {
    int[,] multiDimensionalArray = new int[2, 3]
  }
}
```

Pode-se iniciar com valores usando o mesmo padrão com chaves, a diferença que cada posição terá uma outra chave representando o array interno:

```
int[,] multiDimensionalArray = { { 1, 2, 3 }, { 4, 5, 6 } }
```

Foi criado um array multidimensional em que todas as colunas possuem o mesmo tamanho. Mas também existe outra categoria conhecido por jagged(dentado), em que os arrays variam de tamanho, internamente.

Sintaxe de montagem é um pouco diferente:

```
class PlayingWithArrays
{
  public static void multiDimArrays()
  {
    int[][] jaggedArray = new int[4][];

    jaggedArray[0] = new int[4] { 4, 4, 4, 4 };
    jaggedArray[1] = new int[3] { 3, 3, 3 };
    jaggedArray[2] = new int[5] { 5, 5, 5, 5, 5 };
    jaggedArray[3] = new int[2] { 2, 2 };
  }
}
```

Foi instanciado o array externo no primeiro passo, apenas o primeiro colchetes possui número. Seguindo do aloucamento de cada array em uma posição do array mais externo.\

A principal diferença entre os dois, é o momento da declaração. Para Arrays jagged, utilizamos dois colchetes seguidos `[][]`, enquanto o multidimensional é usado uma vírgula dentro do colchetes `[,]`.

# Funções em C#

- É o encapsulamento de um trecho de código sob uma nomenclatura, Pode ser chamado em qualquer lugar no fluxo, retornando algo ou não.
- É um bloco de código contendo um conjunto de instruções.
- Pode ser chamado de método

Com as funções pode-se dividir em partes, modularizando o programa, para cada função realizar uma ação, trazendo vida ao sistema por meio de um conjunto de funções.

## Estrutura de uma Função em C#

```
Nível de Acessibilidade Retorno Nome (parâmetros)
{ // chave de abertura
  Bloco de código com instruções a serem executadas;
} // chave de fechamento
```

- **Nível de acessibilidade**: É opcional, garante quem pode ou não acessar a função. Usando nível `public` pode ser acessada de qualquer lugar do código; usando `private` só pode ser acessada na mesma classe em que foi criada. Ao omitir essa declaração por padrão seu nível é `private`.
- **Retorno**: Campo Obrigatório. Define se a função retorna algo e qual tipo é retornado.
- **Nome**: Campo Obrigatório. Pode ser definido qualquer nome, mas é indicado usar um nome sugestivo do que é realizado no escopo.
- **Parâmetro**: Campo Opcional. São valores necessário para realizar os procedimentos da funcionalidade, ficam entre parênteses, são separados por vírgula e sua estrutura é baseada em tipo campo e seu nome.
- **Bloco de código**: Tudo que fica entre as chaves. É o escopo de instruções a serem executadas.

```
public double CalculateBMI(int weight, double height)
{
  return weight / (height * height);
}
```

# Instrução try-catch

Forma de tratar exceções que o runtime do dotnet nos fornece, fornece um mecanismo para capturar exceções que ocorrem durante a execução do código, após a instrução por vir a cláusula catch.

Sintaxe:
```
try
{
  // instruções do código
}
catch
{
  // caso aconteça algum erro nas instruções ele usa esse bloco do código para realizar um tratamento no erro.
}
```

É possível criar vários blocos de catch, para especificar como determinada exception vai ser tratada:

```
string[] chemicalProduct = new string[3];

try
{
 chemicalProduct[0] = "Cálcio";
 chemicalProduct[1] = "Zinco";
 chemicalProduct[2] = "Hidrazina";
 chemicalProduct[3] = "Anilina"; 
}
catch (IndexOutOfRangeException ex) 
{
 Console.WriteLine("Erro Específico, sabemos exatamente o motivo do erro.");
}
catch (Exception ex)
{
 Console.WriteLine("Temos a mensagem, porém é um pouco incerto o que ocorreu.");
}
```

Neste exemplo, ao ocorrer o erro de acesso ao index inexistente, ele irá realizar o tratamento diretamente no catch de IndexOUtOfRangeException, e caso ocorra qualquer outro tipo de error, ele será direcionado para o ultimo catch, mais genérico.

Para lançar uma `exception` é usado a instrução throw:

```
throw new Exception()
```

A instrução throw pode ser utilizada sem a expressão do objeto Exception, utilizando-a dentro de um bloco catch, que por sua vez relança a exceção que está sendo manipulada para o fluxo de controle anterior, como no exemplo:

```
using System;

class ExemploThrowRethrow
{
    static void Main()
    {
        try
        {
            DividirPorZero();
        }
        catch (DivideByZeroException ex)
        {
            Console.WriteLine("Ocorreu uma exceção: " + ex.Message);
        }
    }

    static void DividirPorZero()
    {
        try
        {
            int dividendo = 10;
            int divisor = 0;
            int resultado = dividendo / divisor;
        }
        catch (DivideByZeroException)
        {
            Console.WriteLine("Erro: Divisão por zero detectada no método DividirPorZero.");
            // Lança a exceção novamente para o fluxo de controle anterior.
            throw;
        }
    }
}

```

É como realizar um hosting do error para o escopo de cima do catch.\
Caso chamar o throw, fora de um escopo de catch, ele ocorrerá um exceção indicando que uma instrução throw sem argumentos não é permitida fora de uma cláusula catch.

## Instrução finally

É o ultima parte do bloco try-catch de forma opcional, que sempre será executada. Caso essa instrução seja declara antes do catch, ocorrerá um erro em tempo de edição.

```
try
{
  // Código a ser executado
}
catch
{
  // Caso aconteça uma exceção no código dentro do bloco try, aqui vai ser requisitado!
}
finally 
{
  // Aqui sempre vai ser chamado
}
```

Principal objetivo da instrução Finally é realizar a limpeza de ações designadas em um bloco try, sendo uma boa prática durante o desenvolvimento, até mesmo quando não há exceções sendo esperadas.

Usando tr-catch-finally garante maior segurança, qualidade e controle durante o desenvolvimento.

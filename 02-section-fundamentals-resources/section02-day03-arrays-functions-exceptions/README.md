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

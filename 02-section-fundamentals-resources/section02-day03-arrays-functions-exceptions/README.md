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


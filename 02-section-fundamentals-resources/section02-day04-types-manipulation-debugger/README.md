# Conteúdo

- Métodos avançados da classe String
- Classe datetime, suas propriedades e métodos
- Tipos anônimos
- Classes e funções genéricas
- Debugging

# Strings

São usadas em grande parte do desenvolvimento para lidar com cadeia de caracteres que tem uma presentação textual.

```
string name = "Preencher o nome";
```

Originada da classe nativa String, do C# é responsável por conter as funções e propriedades de strings. A class `String` é representada pelo namespace `System`, que contém os atributos, exceções que são fundamentais durante o desenvolvimento.\
Cada caractere de uma string é considerado um `Char`, que representa uma unidade de código UTF-16 (Formato de transformação Unicode de 16bits). Podendo-se afirmar que uma string é uma sequência de Char, representando um cadeia textual.

## Funções da Classe `String`

## Concat()

Usado para concatenação, que é um termo usado no universo de desenvolvimento para designer o processo de uir o valor de diversas strings em somente uma.

```
string textOne = "Você está aprendendo sobre ";
string textTwo = "Strings em C#, ";
string textThree = "e agora sabe concatenar textos utilizando a função Concat()!";

string concatResult = string.Concat(textOne, textTwo, textThree);
Console.WriteLine(concatResult);  
```

## Split()

Usado para separação em múltiplas strings, retornando um array de strings, ocorre de acordo com o separador especificado por parâmetro. Separador é um argumento não obrigatório que tem como objetivo definir qual o termo que vai ser delimitador daquele string para uma matriz de strings.\
Caso não passado nenhum argumento como separador, por padrão o Split vai separar os espaços vazios encontrados na string como uma nova cadeia.

```
string sample01 = "primeiroExemplo";
sample01.Split(); // ["primeiroExemplo"]
string sample02 = "primeiro Exemplo";
sample02.Split(); // ["primeiro", "Exemplo"]
```

## Definindo Separador

```
string sample = "exemplo;exemplo;exemplo";
sample.Split(";"); // ["exemplo", "exemplo", "exemplo"]
```

## IndexOf()

Para encontrar um carácter em uma determinada string e retornar sua posição no índice. O valor retornado é do tipo int, caso não encontrado é retornado `-1`. Retorna o índice da primeira ocorrência. Também é possível indicar a partir de qual índice a busca deve ser iniciar.

```
string sample01 = "exemplo";
sample01.IndexOf("e"); // Encontra o primeiro e, e retornar posição de índice que é 0
string sample02 = "Exemplo por sobrecarga";
sample02.IndexOf("e", 11); // Encontra o e de sobrecarga e retorna sua posição no índice que é 16
```

## Contains()

Verifica se uma determinada string está contida em outra string. Em C$ contains é case sensitive e retorna um boolean.

```
string sample02 = "Exemplo por sobrecarga";
Console.WriteLine(sample02.Contains("Por")); // retorna False
```

## Join()

Tem a responsabilidade de concatenar uma coleção de valores em uma string, deve-se determinar em seu parâmetro, a string separadora e qual coleção.

```
string[] fruits = { "apple", "banana", "cherry" };
string joinedFruits = string.Join(", ", fruits);
// Result: "apple, banana, cherry"

```

Para garantir a interpretação do compilador vale ressaltar que quando atribuído caracteres com aspas simples, se trata apenas de `char`, caracteres e quando usado aspas duplas, estamos indicando que é um tipo string;

```
char singleChar = 'A'; // 'A' is a char
string str = "Hello"; // "Hello" is a string
```

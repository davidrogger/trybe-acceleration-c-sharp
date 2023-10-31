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

## Interpolação de Strings

É uma forma de inserir um valor de uma variável em uma variável com maior legibilidade, facilitando na manutenção.

```
string name = getNameById(123);
Console.WriteLine($"Welcome {name}!");
```

# Datas

Em C# é usada a biblioteca [DateTime](https://learn.microsoft.com/pt-br/dotnet/api/system.datetime?view=net-6.0) para uma forma mais clara de tratar os momentos de tempo.

## O que é um momento de tempo?

É um conjunto informações sobre um ponto no tempo:

- Data. composta por:
  - Dia
  - Mês
  - Ano
- Horário, composto por:
  - Horas
  - Minutos
  - Segundos
  - Milissegundos
- Fuso horário

# DataTime

É um biblioteca dotnet que pertence ao namespace System, não sendo necessário importar diretamente:

```
public class DataUtil
{
  public static void Main(string[ args])
  {
    var date = new DateTime(2023, 31, 10, 12, 05, 0);
    Console.WriteLine(date.ToString()); // 31/10/2023 12:05:00
  }
}
```
Usando o construtor da classe DateTime para criar uma instância com os parâmetros de ano, dia, mês, hora, minuto e segundo e usando o ToString() para imprimir a data.\
A classe DateTime tem uma overload(sobrecarga) de 11 construtores, [lista na documentação](https://learn.microsoft.com/pt-br/dotnet/api/system.datetime?view=net-6.0).
Como o DateTime é uma biblioteca dotnet, o código é compartilhado por todo ambiente dotnet, compatível com todas linguagens suportadas pela plataforma, possibilitando a criação de uma aplicação com momentos de tempo em C# e usa-la em F# ou VB.

## Principais propriedades do DateTime

- `DateTime.Now`\
  Retorna uma instância da classe DateTime com os campos configurados para o momento de tempo exato em que foi chamada.

  ```
    public class DataUtil
    {
        public static void Main(string[] args)
        {
            var dataType = DateTime.Now;
            Console.WriteLine(dataType.GetType()); // System.DateTime
        }
    }
  ```

Seu tipo é DateTime, e sempre que for chamada retornará com a hora que foi chamada.\
Sempre tornar o momento de tempo completo, com data, hora, fuso.

- `DateTime.Date`\
  Acessa o componente da data em uma instância `DateTime` que representa um momento de tempo e retornar uma nova instância de DateTime.

  ```
    public class DataUtil
  {
      public static void Main(string[] args)
      {
          var date = new DateTime(2022, 10, 2, 8, 35, 0);
          var dateOnly = date.Date;
          Console.WriteLine(dateOnly.ToString()); // 02/10/2022
      }
  }
  ```

- `DateTime.Day`\
  Acessa o componente do dia e retorna um valor inteiro entre 1 e 31.

  ```
    public class DataUtil
  {
      public static void Main(string[] args)
      {
          var date = new DateTime(2022, 10, 2, 8, 35, 0);
          var dayOnly = date.Day;
          Console.WriteLine(dayOnly.ToString()); // 2
      }
  }
  ```

- `DateTime.Month`\
  Acessa o componente do mês e returna um valor inteiro entre 1 e 12

  ```
    public class DataUtil
  {
      public static void Main(string[] args)
      {
          var date = new DateTime(2022, 10, 2, 8, 35, 0);
          var monthOnly = date.Month;
          Console.WriteLine(monthOnly.ToString()); // 10
      }
  }
  ```

- `DateTime.Year`\
  Acessa o componente do ano e retornar um valor inteiro entre 1 e 99999
  
  ```
    public class DataUtil
  {
      public static void Main(string[] args)
      {
          var date = new DateTime(2022, 10, 2, 8, 35, 0);
          var yearOnly = date.Year;
          Console.WriteLine(yearOnly.ToString());
      }
  }
  ```

Seguindo um padrão com as propriedades `.Hour`, `.Minute`, `.Second`, `.Millisecond` e `.DayOfWeek`, que retornam os componente de Hora, minute, segundo, milissegundo e dia da semana.

## Principais funções do DateTime

Para manipular objetos de momento de tempo:

- `.Add(TimeSpan value)`\
  Soma um TimeSpan, positivou ou negativo, time representa um intervalo de tempo, [documentação](https://learn.microsoft.com/pt-br/dotnet/api/system.timespan?view=net-6.0).

  ```
    public class DataUtil
  {
      public static void Main(string[] args)
      {
          var today = DateTime.Now;
          var duration = new TimeSpan(36, 0, 0, 0); // 36 dias
          var answer = today.Add(duration);

          System.Console.WriteLine("Hoje é " +today.Day +"/" +today.Month +" - " +today.DayOfWeek);
          System.Console.WriteLine("Daqui a 36 dias será "+answer.Day +"/" +answer.Month +" - " +answer.DayOfWeek);
      }
  }
  ```

  Acima foi adicionado 36 dias a partir do dia de hoje.\
  TimeSpan pode ser negativo:
  ```
    public class DataUtil
  {
      public static void Main(string[] args)
      {
          var today = System.DateTime.Now;
          var duration = new System.TimeSpan(-36, 0, 0, 0);
          var answer = today.Add(duration);

          System.Console.WriteLine("Hoje é " +today.Day +"/" +today.Month +" - " +today.DayOfWeek);
          System.Console.WriteLine("36 atrás era "+answer.Day +"/" +answer.Month +" - " +answer.DayOfWeek);
      }
  }
  ```
  DateTime possui diversos métodos Add para valores específicos:
  - `.AddYears(int value)`: adiciona quantidade de anos a data.
  - `.AddMonths(int value)`: adiciona quantidade de meses a data.
  - `.AddDays(double value)`: adiciona quantidade de dias a data.
  - `.AddHours(double value)`: adiciona quantidade de horas a data.
  - `.AddMinutes(double value)`: adiciona quantidade de minutos a data.
  - `.AddSeconds(double value)`: adiciona quantidade de segundos a data.
  - `.AddMilliseconds(double value)`: adiciona quantidade de milissegundos a data.\

  Alterando o código de cima:
  ```
    public class DataUtil
  {
      public static void Main(string[] args)
      {
          var today = DateTime.Now;
          var answer = today.AddDays(36);

          System.Console.WriteLine("Hoje é " +today.Day +"/" +today.Month +" - " +today.DayOfWeek);
          System.Console.WriteLine("Daqui a 36 dias será "+answer.Day +"/" +answer.Month +" - " +answer.DayOfWeek);
      }
  }
  ```

- `.Compare(DateTime t1, DateTime t2)`\
  Compara e retorna um valor número de:
  - `-1` se a data t1 for anterior à t2
  - `0` se a data t1 for igual à t2
  - `1` se a data t1 for posterior à t2

- `.ToString()`
  Converte um `DateTime` para uma string utilizando critérios padrões do C#\
  Esse método possui métodos com override que pode ser muito úteis:
  - `.ToString(string? format)`\
    Cria uma formatação de saída para o retorno, o C$ oferece os seguintes formatos “d”, “D”, “f”, “F”, “g”, “G”, “m”, “o”, “R”, “s”, “t”, “T”, “u”, “U”, “y”;
    ```
      new DateTime(2008, 6, 15, 21, 15, 07);
    ```
    | Formato | Saída |
    | -- | -- |
    | "d" | 6/15/2008 |
    | "D" | Sunday, June 15, 2008 |
    | "f" | Sunday, June 15, 2008 9:15 PM |
    | "F" | Sunday, June 15, 2008 9:15:07 PM |
    | "g" | 6/15/2008 9:15 PM |
    | "G" | 6/15/2008 9:15:07 PM |
    | "m" | June 15 |
    | "o" | 2008-0615T21:15:07.0000000 |
    | "R" | Sun, 15 2008 21:15:07 GMT |
    | "s" | 2008-06-15T21:15:07 |
    | "t" | 9:15 PM |
    | "T" | 9:15:07 PM |
    | "u" | 2008-06-15 21:15:07Z |
    | "U" | Monday, June 16, 2008 4:15:07 AM |
    | "y" | June, 2008 |

    É possível customizar um formato para `.ToString()`, [documentação](https://learn.microsoft.com/pt-br/dotnet/api/system.datetime.tostring?view=net-6.0#system-datetime-tostring(system-string))

# Tipos Avançados

## Classes e Funções genéricas

Generics é uma forma de flexibilizar a definição de um tipo, ao criar uma classe em que precisamos criar uma lista de algo, podemos definir que ao instanciar é feita a declaração do tipo que será armazenado na lista:

```
public class GenericList<T>
{
    private class Node
    {
        public T Value;
        public Node? Next;

        public Node(T t)
        {
            Value = t;
            Next = null;
        }
    }

    public Node Head;

    public GenericList()
    {
        Head = null;
    }

    public void Add(T input) 
    {
        if (Head == null)
        {
            Head = new Node(input);
            Console.WriteLine("Nó Head criado!");
        }
        else
        {
            //Encontra onde inserir o próximo nó na lista.
            Node lastNode = Head;
            while(lastNode.Next != null)   lastNode = lastNode.Next;

            lastNode.Next = new Node(input);                        
        }
    }
}
```

Nesta listagem temos uma estrutura de dados em nó, a representação do tipo genérico está ao criar a classe `GenericsList<T>` por conversão é usada a letra T, mas podemos usar qualquer outra letra. Sendo possível criar uma lista do tipo `int`, `string`, ou de qualquer tipo desejado.

## Tipos anônimos

São propriedades sem identidade, são uma forma de agrupar propriedades imutáveis associados a uma variável de tipo implícito.

```
var myAnonymousType = new { Amount = 42, Message = "Olá",  Value = 3.95};
```
Devem conter uma ou mais propriedades somente leitura e não podem conter métodos ou eventos.

# Recursos Adicionais

- [Classe String](https://learn.microsoft.com/pt-br/dotnet/api/system.string?view=net-8.0)
- [Construtores da Classe Datetime](https://learn.microsoft.com/pt-br/dotnet/api/system.datetime.-ctor?view=net-6.0)
- [Classes e métodos genéricos](https://learn.microsoft.com/pt-br/dotnet/csharp/fundamentals/types/generics)
- [Depurar um aplicativo de console no Visual Studio Code](https://learn.microsoft.com/pt-br/dotnet/core/tutorials/debugging-with-visual-studio-code?pivots=dotnet-6-0)

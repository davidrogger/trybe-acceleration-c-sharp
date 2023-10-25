# Conteúdo

- Transformação entre tipos de variáveis
- Estruturas de controle no C#
- Estruturas de repetição no C#

## Transformação entre tipos

O casting the uma variável pode ocorrer de diferentes forma, de forma **implícita**, de maneira automática sem intervenção do desenvolvedor no código e **explícito**, quando é necessário escrever a transformação e como irá ocorrer via código.

### Cast Implícito

Se as variáveis forem de tipos compatíveis, ocorre de forma automática pelo compilador:

```
public class Programa
{
    public static void Main()
    {
        int someIntNumber = 51;
        long longNumberCast = someIntNumber;
        
        Console.WriteLine(longNumberCast);
    }
}
```

A variável do tipo `long` é compatível com a variável `int`, por se tratarem de números inteiros que cabem 32bits, int tem no máximo 32 bits, já long 64bits, não seria possível fazer o cast do long ao int.

### Cast Explícito

Existem casos que é necessário indicar a ação a ser tomada:

```
public class Program
{
    public static void Main()
    {
        long someLongNumber = 516144066604654;
        int intNumber = someLongNumber;

        Console.WriteLine(intNumber);
    }
}
```

O espaço de memória não é compatível, dessa forma para contornar o erro, é usado o cast para realizar a atribuição, porém haverá perda de informação, e não será notificado sobre perda.

```
public class Program
{
    public static void Main()
    {
        long someLongNumber = 516144066604654;
        int intNumber = (int) someLongNumber;
        
        Console.WriteLine(intNumber); // 66775150
    }
}
```

Outra conversão é por meio do `Convert.ToInt32`.

```
public class Program
{
    public static void Main()
    {
        long someLongNumber = 516144564564654;
        int intNumber = Convert.ToInt32(someLongNumber);

        Console.WriteLine(intNumber);
    }
}
```

Usando o Convert ele ocorre um erro assim como no cast implícito, notifica que o número não tem espaço para variável:

```
Unhandled exception. System.OverflowException: Value was either too large or too small for an Int32.
   at System.Convert.ThrowInt32OverflowException()
   at System.Convert.ToInt32(Int64 value)
   at Program.Main() in /Users/user/C#/teste cod/Program.cs:line 6
```

Caso seja possível realizar a conversão, ele a realiza.

## Conversão de string para números

É possível realizar a conversão de strings para números, em algumas situações:

```
public class Programa
{
    public static void Main()
    {
        string someString = "42";
        int convertInt = Convert.ToInt32(someString);

        Console.WriteLine(convertInt);
    }
}
```

Porém não é possível garantir que o conteúdo pode ser convertido para número, para isso é usado o `TryParse`.

```
bool canConvert = Int32.TryParse(userEntry, out int valueConverted)
```

Ele retorna um boolean, se é possível a conversão, e pode-se coletar a conversão no segundo parâmetro. Caso seja false, o segundo parâmetro retorna zero.

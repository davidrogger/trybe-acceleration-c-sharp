# Conteúdo

- Orientação à objetos
- Classes no C#
- Métodos estáticos

## Abstração: as Classes em C#

Em síntese é um tipo customizado que contém a abstração de um objeto.
Utilizada em qualquer linguagem orientada a objetos. Todo código é baseado em abstrair, nas propriedades e métodos da sua classe as características e comportamentos do objeto.\
É uma boa prática criar cada classe em seu próprio arquivo.

Criando uma classe vazia:
```
class Rocket
{

}
```

Para que uma classe possa ser utilizada em outros lugares do código ela precisa ser instanciada, pois a classe nada mais é que um molde, e é necessário desse molde criar o objeto que seria a instancia.\

Adicionando propriedade a classe:
```
class Rocket
{
  public string Name { get; set; }
}
```

Instanciando:
```
var rocket1 = new Rocket();
var rocket2 = rocket1;

rocket1.Name = "Apollo 11";
rocket2.Name = "Falcon 9";

Console.WriteLine(rocket1.Name);
```

Ao fazer a atribuição `var rocket2 - rocket1;`, apenas copiamos a referência à instância de foguete criada na atribuição da variável. Por se tratar de reference types quando lidando com classes.

# Construtores

São métodos chamados toda vez que uma instância de classe é criada, mesmo sem definir um construtor customizado. Por padrão o construtor padrão não aceitará nenhum parâmetro nem propriedades.

```
class Rocket
{
  string Name { get; set; }

  public Rocket(string name)
  {
    Name = name;
  }
}
```

Dessa forma, ao iniciar a instância, o construtor exige que seja passado nome, para ser atributo ao atributo name do objeto.\
Declaração de Public no construtor é necessário caso seja criado uma instância da classe a partir de outro lugar que não seja a própria classe.

Em casos necessários que se é usado o mesmo nome para um campo da classe ou parâmetro, utiliza-se o operador this:

```
class Rocket
{
  string name;

  public Rocket(string name)
  {
    this.name = name;
  }
}
```

O uso no `this` tem o objetivo de explicitar o acesso a propriedade ou função da própria instância, o que permite evitar uma ambiguidade. É raro o uso do `this` para definir campos, a prática mais difundida é declarar usando underscore antes do nome.

```
class Rocket
{
  string _name;

  public Rocket(string name)
  {
    _name = name;
  }
}
```

Para evitar que seja confundido os campos da classe com as variáveis e parâmetros utilizados nos métodos.\

Para instanciar uma classe de forma simples é usado a palavra chave `new`:

```
var pessoas = new Client();
```

`new` determina que o construtor da classe seja invocado.

## Classes e instâncias na POO

O comportamento dos objetos é definido nos métodos das classes, enquanto o seu estado é determinado pelos valores dos seus campos e propriedades.

## Classes e métodos estáticos

### get e set

Métodos especiais para coleta e modificação de atributos do objeto.

- Getters: são métodos de acesso que usam a palavra chave get para definir a forma de se retornar o valor de determinada propriedade.
- Setters: são métodos de acesso que utilizam a palavra chave set para definir formas de se modificar o valor de determinada propriedade.

```
class Rocket
{
    int Fuel { get; set; }
}
```

Forma acima gera uma propriedade auto implementada, o próprio compilador vai gerar um campo privado para a classe, que será acessado pelos getters e setters.

Declaração implícita:
```
class Person
{
    string Name { get; set; }
}
```

Declaração explicita:
```
class Person
{
    string _name;

    public string Name
    {
        get { return _name; }
        set { _name = value; }
    }
}
```

## Usando métodos para instanciar classes

Em C# é possível usar uma ferramentada chamada object initializer, que permite que seja instanciado um objeto com a atribuição de valores de suas propriedades sem invocar diretamente o construtor.
Caso seja necessário estabelecer uma classe que representa um objeto simples.

```
new <ClassName>
{
    Property = someValue,
    Property2 = anotherValue
    ...
};
```

```
class Cake
{
    public string Size { get; set; }
    public string Flavour { get; set; }
}

Cake chocolateCake = new Cake
    {
      Size = "10",
      Flavour = "Chocolate"
    };
```

## Modificador `static`

São métodos independentes da instancia, para acessar este método deve-se usar a própria classe.Sendo associados à classe onde são declarados com um todo.

```
public static class Sample
{
  public static string[] exercises = { "getter", "setter", "static" };
}
```

Ao tentar instanciar uma classe static, ocorre um erro de compilação.

Para acessar os valores de exercises é usada a propria classe.
```
Sample.exercises
```

## Recursos adicionais

- [Programação orientada a objeto (C#)](https://learn.microsoft.com/pt-br/dotnet/csharp/fundamentals/tutorials/oop)
- [Introdução às classes](https://learn.microsoft.com/pt-br/dotnet/csharp/fundamentals/types/classes)
- [get e set(Referência de C#)](https://learn.microsoft.com/pt-br/dotnet/csharp/language-reference/keywords/get)
- [Classes static e membros de classes static](https://learn.microsoft.com/pt-br/dotnet/csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members)
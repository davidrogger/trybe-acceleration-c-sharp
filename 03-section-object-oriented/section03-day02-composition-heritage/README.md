# Conteúdo

- Composição
- Herança
- Polimorfismo
- Classes Abstratas
- Modificadores de Acesso
- Estruturas Avançadas

# Composição

É um conceito da orientação a objetos que permite definir que uma classe mais complexa é composta por outras classes, possibilitando separar conceitos e desacoplar funções, tornando a classe mais concisa e modular.

```
class Car
{
    public double TopSpeed { get; set; }
    public bool IsAutomatic { get; set; }
    public int NumberOfSeats { get; set; }

    public int EngineHorsepower { get; set; }
    public int EngineTorque { get; set; }
    public int EngineCapacity { get; set; }
    public bool IsEngineStarted { get; set; }

    public void Drive(double distanceKm, double speed)
    {
        if (speed > TopSpeed)
            Console.WriteLine("Your car can't go that fast!");
        else if (!IsEngineStarted)
            Console.WriteLine("Your car isn't turned on!");
        else
        {
            var time = distanceKm / speed;
            Console.WriteLine($"You arrived in {time} hours.");
        }
    }

    public void StartEngine()
    {
        if (IsEngineStarted)
            Console.WriteLine("The engine is already started!");
        else
            IsEngineStarted = true;
    }

    public void StopEngine()
    {
        if (!IsEngineStarted)
            Console.WriteLine("The engine is already stopped!");
        else
            IsEngineStarted = false;
    }
}
```

Dividindo responsabilidade usando o conceito de composição:

```
class Engine
{
    public int Horsepower { get; set; }
    public int Torque { get; set; }
    public int Capacity { get; set; }
    public bool IsStarted { get; set; }

    public void Start()
    {
        if (IsStarted)
            Console.WriteLine("The engine is already started!");
        else
            IsStarted = true;
    }

    public void Stop()
    {
        if (!IsStarted)
            Console.WriteLine("The engine is already stopped!");
        else
            IsStarted = false;
    }
}

class Car
{
    public double TopSpeed { get; set; }
    public bool IsAutomatic { get; set; }
    public int NumberOfSeats { get; set; }
    public Engine Engine { get; set; } = new Engine();

    public void Drive(double distanceKm, double speed)
    {
        if (speed > TopSpeed)
            Console.WriteLine("Your car can't go that fast!");
        else if (!Engine.IsStarted)
            Console.WriteLine("Your car isn't turned on!");
        else
        {
            var time = distanceKm / speed;
            Console.WriteLine($"You arrived in {time} hours.");
        }
    }

    public void StartEngine() => Engine.Start();

    public void StopEngine() => Engine.Stop();
}
```

Agora se for necessário criar uma classe moto, que usa a mesma lógica de motor do carro, só é necessário fazer a composição de engine.

# Herança

Para estabelecer uma relação entre duas classes de modo a ter uma melhor organização no código.\
Estabelece uma hierarquia entre duas classes de modo que uma classe mais específica, chamada de derivada ou subclasse, receba automaticamente todos os métodos e propriedades de uma classe mais geral, também chamada de base ou superclasse, sem precisar defini-los novamente.
Sintaxe para criar uma classe derivada é `<ClasseDerivada> : <ClasseBase>`;

```
public class Car : Vehicle
{

}
```

Quando há necessidade de modificar a implementação de algum método da herança, pode ser realizado um override, se for declarado na superclasse que o método é virtual.

- `virtual`: modificador define um membro como virtual
    - Classes não podem receber o modificador `virtual`
    - Métodos virtuais possuem implementação, que podem ou não ser sobrescritas na classe derivada
- `abstract`: modificador que define uma classe ou membro como abstrato.
    - Apenas classes abstratas podem ter métodos abstratos.
    - Métodos abstratos não possuem implementação e devem sempre ser sobrescritos.

# Interfaces

É comum a implementação de objetos que não possuímos conhecimento sobre. Sendo representado por uma implementação ou que nenhum implementação tenha sido criada, de modo que só temos ideia do que ele representa, sendo necessário o uso de uma estrutura intermediária, que diga quais os elementos mínimos que essa abstração deverá ter para ser válida, mas sem a implementação direta. Em C# é chamado de interface, não define ou instancia, sendo mais um contrato, que define quais comportamentos mínimos o objeto que iremos utilizar deve definir para poder ser utilizado naquele local. Quando uma classe implementa uma interface ela, segue às regras definidas por ela.\
Apesar de ter a função de descrever métodos e comportamentos, a interface não estabelece uma relação de herança, pois não há uma relação de tipo/subtipo.

```
interface IGreeter
{
    void SayGreeting(string greeting);
}
```

Por convenção da comunidade também é adotado o uso do I, em todo inicio do nome da uma interface, para melhor identificação.

A partir da ver~sao 8, o C# permite a criação de membros virtuais, como implementações concretas, no corpo da própria interface. Diferente da herança, caso uma interface possua implementações de membros por padrão ela será virtual, sendo possível sobrescrever.

```
public interface IStartable
{
    void Start()
    {
        Console.WriteLine("Item started");
    }
}
```

Só é possível acessar a implementação padrão de um método de uma interface em uma referência à própria interface, não a um tipo específico, mesmo que esse tipo a implemente.

```
public class Engine : IStartable
{
}
```

```
IStartable engine = new Engine();
engine.Start();
```

Definindo o objeto engine utilizando seu próprio tipo `Engine engine = new Engine()` ou implícita `var engine = new Engine()`, o código não irá funcionar.\

É possível também a declaração de multiplas `interfaces`:

```
public interface IStartable
{
    void Start();
}

public interface IStoppable
{
    void Stop();
}

public class Engine : IStartable, IStoppable
{
    public void Start() => Console.WriteLine("Engine started!");
    public void Stop() => Console.WriteLine("Engine stopped!");
}
```

# Polimorfismo

Quando falando de orientação a objetos, estamos falando de um paradigma no qual, essencialmente, quase todas a lógica da aplicação é encapsulada em objetos criados a partir de abstrações.
Tornando possível que mais de uma abstração possa responder a uma mesma mensagem, com implementações e retornos independentes entre si, quando objetos de tipos diferentes podem ser utilizados no mesmo contexto, sem que isso gere problemas de compatibilidade.

```
public interface Player
{
    public void Play(string mediaName);
}
```

```
public class AudioPlayer
{
    public IPlayer Player { get; set; }

    public void MusicPlayer(IPlayer player)
    {
        Player = player;
    }

	public void PlaySong(string songName)
	{
	    Player.Play(songName)
	}

	public void PlayPodcast(string podcastName)
	{
	    Player.Play(podcastName)
	}
}
```

# Classes abstratas

Classes estáticas não são as únicas classes que não são instanciáveis, temos também as classes abstratas, que são aquelas que implementam todos os seus métodos e que não são implementadas diretamente, sendo ponto de partida para classes derivadas que, por sua vez, serão instanciadas.
Herdando uma classe abstrata, não é herdado apenas as funcionalidades de métodos já implementados, mas também por meio dos métodos abstratos, diretrizes de implementação, que definem apenas o formato das mensagens que a classe herdeira deve ser capaz de receber.

# Modificadores de acesso C#

- public
- protected
- private

## Public

Qualquer parte do código pode referencias esse item se estiver no seu escopo. Atribuir sempre atributos e métodos como públicos não é uma boa prática no mercado, pois permite que erros das pessoas desenvolvedora causem mal funcionamento do sistema ou até traga riscos à segurança dos dados.

```
public class MusicConverter
{
    public static void ToMp3()
    {
        //...
    }
    public static void ToWav()
    {
        //...
    }
    // ...
}
```

## Protected

Permite o acesso e referência para itens na mesma classe ou em classes herdeiras.

## Private

É o modificador padrão de atributos membros em C#, ele permite o acesso para itens apenas na mesma classe.

# Organizando TIpos em C#

Namespace é uma forma de organizar tipos definidos, como classes, structs, interfaces e enums em um mesmo conjunto.
Ao organizar tios em um mesmo conjunto, podemos definir domínios específicos em uma aplicação, facilitando o processo de encontrar tipos ou utilizá-los em diferentes artes do sistema. Sendo uma forma muito usada em C# até mesmo pelo framework dotnet.

```
namespace MyNamespace
{
    public class Car
    {
        // Código da minha classe Car
    }
}
```

Foi organizado a classe `Car` dentro do namespace `MyNamespace`, ficando acessível como `MyNamespace.Car` ou utilizando a keyword using.

```
var myCar = new MyNamespace.Car();
```

```
using MyNamespace;

var myCar = new Car();
```

## Structs

São estruturas de dados em C# onde é possível criar objetos de forma parecida com class, porém simplificada.

Em C#, temos duas categorias de tipos de variáveis, os Tipos de valor e os Tipos de referência.

- valor: variáveis que possuem seu valor armazenado diretamente, a variável em si é aquele valor que ela representa e não uma referencia para o valor em outra parte da memória. Sendo eles: `int`, `float`, `double`, `char`, `bool`.
- referencia: armazenam uma referência ao seu valor e não o valor propriamente dito, e isso tem consequências importantes. Por exemplo, duas variáveis de tipo de referência podem se referenciar a um mesmo valor armazenado na memória. Sendo eles: `classes`, `interfaces`, `string`, `action`.

A sintaxe de structs é bem similar a de classe, usando a palavra reservada `struct`, seguida do nome da classe, e em seguida descreve o conteúdo da estrutura dentro de chaves `{}`.

```
struct Coordinate
{
    public double Latitude;
    public double Longitude;
}
```
Pode-se definir um construtor assim como em classes:

```
struct Coordinate
{
    public double Latitude;
    public double Longitude;

    public Coordinate(double latitude, double longitude)
    {
        Latitude = latitude;
        Longitude = longitude;
    }
}
```
Também possuem modificadores de acesso, public, private e protected.

E seu uso é igual ao de uma classe;
```
// someLocation irá inicializar com os valores de latitude e longitude fornecidos
Coordinate someLocation = new Coordinate(-19.9222072, -43.9339879);

// anotherLocation irá inicializar com os valores de latitude e longitude iguais a 0
Coordinate anotherLocation = new Coordinate();
```

Mesmo não existindo um construtor explícito que não recebe nenhum parâmetro, é possível realizar a instanciação, justamente pelo fato de existirem. Isso é possível porque essa `struct` contém apenas propriedades que possuem um valor inicial padrão, no caso `double`, seu valor padrão é 0, anotherLocation será instanciado com Latitude e Longitude igual a 0.

## Enum

São estruturas de dados em C# que são utilizadas para melhorar a legibilidade do código construído. Podemos agrupar várias constantes nomeadas em um novo tipo, como se pertencesse a um mesmo grupo.

```
enum PaymentType
{
    // Credit tem valor 0
    Credit = 0,

    // Debit tem valor 1
    Debit = 1
}
```

```
class Order
{
    public PaymentType PayType
}
```

```
Order myOrder = new Order();

myOrder.PayType = PaymentType.Credit;
```

Não é necessário definir os valores das constantes de um Enum. Caso não seja definido, os valores serão inteiros, começando do 0 seguindo de forma crescente.
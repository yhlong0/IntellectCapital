# Head First Design Pattern

1. OOP Basics: inheritance, encapsulation(use private vars to store data, provide public methods), polymorphism, and abstraction(hide complex implementation details), ask chatGPT for examples
2. OO Principles:
    - Encapsulate what varies
    - Favor Composition over Inheritance
    - Program to interfaces, not implementation
    - Strive for loosely coupled designs between objects that interact
    - Class should be closed for modification but open for extension.
    - If you use new keyword, you'll be holding a reference to a concrete class. Use a factory to get around that!
    - If you derive from a concrete class, you're depending on a concrete class. Derive from an abstraction, like an interface or an abstract class.
    - No method should override an implemented method of any of its base classes. (shape -> draw(), circle -> override draw())
3. Strategy Pattern: Defining an interface, abstract class (Strategy) that represents a family of behaviors or methods(Algorithms). Concrete implementations of this interface represent specific behaviors, functions, or methods. By programming to the interface rather than to a specific implementation, you can switch out one behavior for another at runtime without changing the calling code. When you have a group of behaviors would change depending on context(all ducks make sounds, but different sounds). Instead of putting methods in superclass and child inherited then overriding them one by one, some of the overrides would be the same(wood duck and steel duck both not making sounds). Strategy Pattern is good for solving this.
```java
// Define the Strategy(interface)
public interface PaymentStrategy {
    void processPayment(double amount);
}

// Implement concrete strategies
public class CreditCardPayment implements PaymentStrategy {
    @Override
    public void processPayment(double amount) {
        // Logic for processing credit card payment
        System.out.println("Processed credit card payment of: $" + amount);
    }
}

public class PaypalPayment implements PaymentStrategy {
    @Override
    public void processPayment(double amount) {
        // Logic for processing PayPal payment
        System.out.println("Processed PayPal payment of: $" + amount);
    }
}

// Context class
public class PaymentProcessor {
    private PaymentStrategy strategy;

    public PaymentProcessor(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void setStrategy(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void executePayment(double amount) {
        strategy.processPayment(amount);
    }
}

// Usage

public class Main {
    public static void main(String[] args) {
        PaymentProcessor processor = new PaymentProcessor(new CreditCardPayment());
        processor.executePayment(100.00);

        processor.setStrategy(new PaypalPayment());
        processor.executePayment(200.00);
    }
}
```

5. Observer Pattern: defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically. 
```csharp
// Observer interface
public interface IObserver
{
    void Update(float temperature, float humidity, float pressure);
}

// Subject interface
public interface ISubject
{
    void RegisterObserver(IObserver o);
    void RemoveObserver(IObserver o);
    void NotifyObservers();
}

public class WeatherStation : ISubject
{
    private List<IObserver> observers;
    private float temperature;
    private float humidity;
    private float pressure;

    public WeatherStation()
    {
        observers = new List<IObserver>();
    }

    public void RegisterObserver(IObserver o)
    {
        observers.Add(o);
    }

    public void RemoveObserver(IObserver o)
    {
        observers.Remove(o);
    }

    public void NotifyObservers()
    {
        foreach (var observer in observers)
        {
            observer.Update(temperature, humidity, pressure);
        }
    }

    public void MeasurementsChanged()
    {
        NotifyObservers();
    }

    public void SetMeasurements(float temperature, float humidity, float pressure)
    {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        MeasurementsChanged();
    }
}

public class CurrentConditionsDisplay : IObserver
{
    private float temperature;
    private float humidity;
    private ISubject weatherStation;

    public CurrentConditionsDisplay(ISubject weatherStation)
    {
        this.weatherStation = weatherStation;
        weatherStation.RegisterObserver(this);
    }

    public void Update(float temperature, float humidity, float pressure)
    {
        this.temperature = temperature;
        this.humidity = humidity;
        Display();
    }

    public void Display()
    {
        Console.WriteLine($"Current conditions: {temperature}F degrees and {humidity}% humidity");
    }
}

// ... You can create more displays like `StatisticsDisplay`, `ForecastDisplay`, etc.

class Program
{
    static void Main(string[] args)
    {
        WeatherStation weatherStation = new WeatherStation();

        CurrentConditionsDisplay currentDisplay = new CurrentConditionsDisplay(weatherStation);

        weatherStation.SetMeasurements(80, 65, 30.4f);  // This should update the `currentDisplay` automatically
        // ... Add more measurements and displays as needed
    }
}
```
6. Decorator Pattern: Attaches additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.
```csharp
public abstract class Coffee
{
    public abstract double Cost();
}

public class SimpleCoffee : Coffee
{
    public override double Cost()
    {
        return 5.0;
    }
}

public abstract class CoffeeDecorator : Coffee
{
    protected Coffee _coffee;
    
    public CoffeeDecorator(Coffee coffee)
    {
        _coffee = coffee;
    }
    
    public override double Cost()
    {
        return _coffee.Cost();
    }
}

// Implement concrete decorators (add-ons for the coffee)
public class MilkDecorator : CoffeeDecorator
{
    public MilkDecorator(Coffee coffee) : base(coffee) { }

    public override double Cost()
    {
        return _coffee.Cost() + 2.0;
    }
}

public class SugarDecorator : CoffeeDecorator
{
    public SugarDecorator(Coffee coffee) : base(coffee) { }

    public override double Cost()
    {
        return _coffee.Cost() + 1.0;
    }
}

public class Program
{
    public static void Main()
    {
        Coffee simpleCoffee = new SimpleCoffee();

        Coffee milkCoffee = new MilkDecorator(simpleCoffee);
        Console.WriteLine($"Cost of milk coffee: {milkCoffee.Cost()}");

        Coffee sugarMilkCoffee = new SugarDecorator(milkCoffee);
        Console.WriteLine($"Cost of sugar milk coffee: {sugarMilkCoffee.Cost()}");
    }
}

```
7. The Factory Pattern: to provide an interface for creating objects but allowing subclasses to alter the type of objects that will be created.
    - Simple Factory: a simple way to encapsulate the logic for object creation, if you ever need to make changes to the creation logic (e.g., add a new type of pizza), you won’t have to modify the code everywhere the objects are being created, just the factory.
    - Factory Method Pattern: define an interface for creating objects, but it's derived class to implement the method and decide which class to instantiate. In other words, instead of calling a constructor directly to create an object, a method is used to create the object, and subclasses decide which class to instantiate.
    - Abstract Factory Pattern: 
```csharp
# simple factory

public class Pizza
{
    public string Type { get; set; }
    // ... other properties and methods like Bake, Cut, Box etc.
}

public class NYPizza : Pizza
{
    public NYPizza()
    {
        Type = "New York Style Pizza";
    }
    // ... other specific properties or methods for NY Pizza
}

public class CaliforniaPizza : Pizza
{
    public CaliforniaPizza()
    {
        Type = "California Style Pizza";
    }
    // ... other specific properties or methods for California Pizza
}

public class SimplePizzaFactory
{
    public Pizza CreatePizza(string type)
    {
        Pizza pizza = null;
        if (type == "NY")
        {
            pizza = new NYPizza();
        }
        else if (type == "California")
        {
            pizza = new CaliforniaPizza();
        }
        return pizza;
    }
}

public class PizzaStore
{
    SimplePizzaFactory factory;

    public PizzaStore(SimplePizzaFactory factory)
    {
        this.factory = factory;
    }

    public Pizza OrderPizza(string type)
    {
        Pizza pizza;

        pizza = factory.CreatePizza(type);

        // These are hypothetical methods that every Pizza might have
        pizza.Prepare();
        pizza.Bake();
        pizza.Cut();
        pizza.Box();

        return pizza;
    }
}

var factory = new SimplePizzaFactory();
var store = new PizzaStore(factory);

Pizza myNYPizza = store.OrderPizza("California");
Console.WriteLine($"Ordered a {myPizza.Type}");

Pizza myCAPizza = store.OrderPizza("NY");
Console.WriteLine($"Ordered a {myPizza.Type}");

# Factory Method Pattern

public abstract class Pizza
{
    public string Name { get; set; }
    // ... other properties and methods like Prepare, Bake, Cut, Box
}

public class NYCheesePizza : Pizza
{
    public NYCheesePizza()
    {
        Name = "New York Style Cheese Pizza";
    }
}

public class CaliforniaCheesePizza : Pizza
{
    public CaliforniaCheesePizza()
    {
        Name = "California Style Cheese Pizza";
    }
}

public abstract class PizzaStore
{
    public Pizza OrderPizza(string type)
    {
        Pizza pizza = CreatePizza(type);
        pizza.Prepare();
        pizza.Bake();
        pizza.Cut();
        pizza.Box();
        return pizza;
    }

    // This is the Factory Method
    protected abstract Pizza CreatePizza(string type);
}

public class NYPizzaStore : PizzaStore
{
    protected override Pizza CreatePizza(string type)
    {
        if (type == "cheese")
        {
            return new NYCheesePizza();
        }
        // You can expand for other types like "pepperoni", "clam", etc.
        return null;
    }
}

public class CaliforniaPizzaStore : PizzaStore
{
    protected override Pizza CreatePizza(string type)
    {
        if (type == "cheese")
        {
            return new CaliforniaCheesePizza();
        }
        // Expand for other types
        return null;
    }
}

# Using the Factory:
var nyStore = new NYPizzaStore();
Pizza pizza1 = nyStore.OrderPizza("cheese");
Console.WriteLine($"Ordered a {pizza1.Name}\n");

var californiaStore = new CaliforniaPizzaStore();
Pizza pizza2 = californiaStore.OrderPizza("cheese");
Console.WriteLine($"Ordered a {pizza2.Name}\n");


```


9. The Dependency Inversion Principle: Depend upon abstractions, Do not depend upon concrete classes. Our high-level components(PizzaStore) should not depend on our low-level components(pizza), rather, they should both depend on abstractions.
```csharp
// bad example, AppService depends on the Logger class, if you want to
// log to a file or a db, you'll need to modify the 'AppService class'
// violates the Open-Closed Principle
public class Logger
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }
}

public class AppService
{
    private Logger _logger = new Logger();

    public void DoSomething()
    {
        // Some business logic...
        _logger.Log("Operation completed.");
    }
}

//good example, AppService no longer depends on a specific logger.
//
public interface ILogger
{
    void Log(string message);
}

public class ConsoleLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine(message);
    }
}

public class FileLogger : ILogger
{
    private string _filePath = "log.txt";

    public void Log(string message)
    {
        File.AppendAllText(_filePath, message + Environment.NewLine);
    }
}

public class AppService
{
    private ILogger _logger;

    public AppService(ILogger logger)
    {
        _logger = logger;
    }

    public void DoSomething()
    {
        // Some business logic...
        _logger.Log("Operation completed.");
    }
}

var serviceWithConsoleLogger = new AppService(new ConsoleLogger());
var serviceWithFileLogger = new AppService(new FileLogger());

```
10. Abstract Factory
```csharp
# interfaces for pizza ingredients: 
public interface IDough
{
    string GetDough();
}

public interface ISauce
{
    string GetSauce();
}

public interface ICheese
{
    string GetCheese();
}

# concrete implementations for these ingredients:
public class ThickDough : IDough
{
    public string GetDough()
    {
        return "Thick dough";
    }
}

public class ThinDough : IDough
{
    public string GetDough()
    {
        return "Thin dough";
    }
}

public class TomatoSauce : ISauce
{
    public string GetSauce()
    {
        return "Tomato sauce";
    }
}

public class CheeseSauce : ISauce
{
    public string GetSauce()
    {
        return "Cheese sauce";
    }
}

public class Mozzarella : ICheese
{
    public string GetCheese()
    {
        return "Mozzarella cheese";
    }
}

public class Cheddar : ICheese
{
    public string GetCheese()
    {
        return "Cheddar cheese";
    }
}

# define an abstract factory interface for creating pizzas:
public interface IPizzaIngredientFactory
{
    IDough CreateDough();
    ISauce CreateSauce();
    ICheese CreateCheese();
}

# create concrete factories that implement this interface:
public class ItalianPizzaIngredientFactory : IPizzaIngredientFactory
{
    public IDough CreateDough()
    {
        return new ThinDough();
    }

    public ISauce CreateSauce()
    {
        return new TomatoSauce();
    }

    public ICheese CreateCheese()
    {
        return new Mozzarella();
    }
}

public class AmericanPizzaIngredientFactory : IPizzaIngredientFactory
{
    public IDough CreateDough()
    {
        return new ThickDough();
    }

    public ISauce CreateSauce()
    {
        return new CheeseSauce();
    }

    public ICheese CreateCheese()
    {
        return new Cheddar();
    }
}

# Pizza class that uses the abstract factory to get ingredients:
public class Pizza
{
    private IDough dough;
    private ISauce sauce;
    private ICheese cheese;

    public Pizza(IPizzaIngredientFactory factory)
    {
        dough = factory.CreateDough();
        sauce = factory.CreateSauce();
        cheese = factory.CreateCheese();
    }

    public void Prepare()
    {
        Console.WriteLine($"Preparing pizza with {dough.GetDough()}, {sauce.GetSauce()}, and {cheese.GetCheese()}");
    }
}

# create pizza using different factories:
class Program
{
    static void Main(string[] args)
    {
        IPizzaIngredientFactory italianFactory = new ItalianPizzaIngredientFactory();
        Pizza italianPizza = new Pizza(italianFactory);
        italianPizza.Prepare();  // Output: Preparing pizza with Thin dough, Tomato sauce, and Mozzarella cheese

        IPizzaIngredientFactory americanFactory = new AmericanPizzaIngredientFactory();
        Pizza americanPizza = new Pizza(americanFactory);
        americanPizza.Prepare();  // Output: Preparing pizza with Thick dough, Cheese sauce, and Cheddar cheese
    }
}
```
11. Singleton Pattern: ensures that a class has only one instance and provides a global point to access it. This pattern is useful in scenarios like a database connection, logging, driver object, caching, thread pools, or configuration manager.
```csharp
public sealed class Singleton
{
    private static Singleton _instance = null;
    private static readonly object _lock = new object();
    
    private Singleton()
    {
        // Constructor is 'private' so that
        // it is not instantiated more than once.
    }

    public static Singleton Instance
    {
        get
        {
            lock (_lock)
            {
                if (_instance == null)
                {
                    _instance = new Singleton();
                }
                return _instance;
            }
        }
    }

    public void DoSomething()
    {
        Console.WriteLine("Singleton instance method called.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Singleton instance1 = Singleton.Instance;
        instance1.DoSomething();  // Output: Singleton instance method called.

        Singleton instance2 = Singleton.Instance;
        instance2.DoSomething();  // Output: Singleton instance method called.

        if (instance1 == instance2)
        {
            Console.WriteLine("Both instances are the same.");  // Output: Both instances are the same.
        }
    }
}

```
12. Command Pattern: Encapsulates a request as an object, thereby parameterizing clients with queues, requests, and operations. It also allows for the support of undoable operations. Separates the object that issues a command from the object that actually performs the command, providing additional functionalities like queuing commands, logging, or even supporting undoable operations.
```csharp
using System;

// Command Interface
public interface ICommand
{
    void Execute();
    void Undo();
}

// ConcreteCommand
public class NoCommand : ICommand
{
    public void Execute() {}
}

public class LightOnCommand : ICommand
{
    private Light light;

    public LightOnCommand(Light light)
    {
        this.light = light;
    }

    public void Execute()
    {
        light.TurnOn();
    }
}

public class CeilingFanHighCommand : ICommand
{
    private CeilingFan ceilingFan;
    private int prevSpeed;

    public CeilingFanHighCommand(CeilingFan ceilingFan)
    {
        this.ceilingFan = ceilingFan;
    }

    public void Execute()
    {
        prevSpeed = ceilingFan.getSpeed();
        ceilingFan.high();
    }

    public void Undo()
    {
        if(prevSpeed == CeilingFan.HIGH) {
            ceilingFan.high();
        } else if (prevSpeed == CeilingFan.MEDIUM) {
            ceilingFan.medium()
        }....
    }
}

// Receiver
public class Light
{
    public void TurnOn()
    {
        Console.WriteLine("Light is on");
    }

    public void TurnOff()
    {
        Console.WriteLine("Light is off");
    }
}

public class CeilingFan
{
    public const int HIGH = 3;
    public const int MEDIUM = 2;
    public const int LOW = 1;
    public const int OFF = 0;
    String location;
    int speed;

    public CeilingFan(String location)
    {
        this.location = location;
        speed = OFF;
    }

    public void high()
    {
        speed = HIGH;
        // code to set fan to high        
    }

    public void medium()
    {
        speed = MEDIUM;
        // code to set fan to medium        
    }

    public void off()
    {
        speed = OFF;
        // code to set fan to off        
    }

    public int getSpeed()
    {
        return speed;
    }
}


// Invoker
public class RemoteControl
{
    private ICommand[] onCommands;
    private ICommand[] offCommands;
    private ICommand undoCommand;

    public RemoteControl()
    {
        onCommands = new ICommand[7];
        offCommands = new ICommand[7];
        ICommand noCommand = new NoCommand();

        for(int i = 0; i < 7; i++) {
            onCommands[i] = noCommand;
            offCommands[i] = noCommand;
        }
        undoCommand = noCommand;
    }

    public void SetCommand(int slot, ICommand onCommand, ICommand offCommand)
    {
        this.onCommands[slot] = onCommand;
        this.offCommands[slot] = offCommand;
    }

    public void PressOnButton(int slot)
    {
        onCommands[slot].Execute();
        undoCommand = onCommands[slot];
    }

    public void PressOffButton(int slot)
    {
        offCommands[slot].Execute();
        undoCommand = offCommands[slot];
    }

    public void PressUndoButton()
    {
        undoCommand.Undo();
    }
}

// Client Code
public class Program
{
    static void Main(string[] args)
    {
        Light light = new Light();
        LightOnCommand lightOn = new LightOnCommand(light);

        CeilingFan ceilingFan = new CeilingFan("Living Room");
        CeilingFanHighCommand = ceilingFanHigh = new CeilingFanHighCommand(ceilingFan);

        RemoteControl remote = new RemoteControl();

        remote.SetCommand(lightOn);
        remote.PressButton();  // Output: "Light is on"


    }
}
```
13. How can I implement a history of undo operations, able to press the undo button multiple times: keep a stack of previous commands, whenever undo is pressed, pop the first item off the stack.
14. When implementing party mode, instead of hardcoding the part mode into party command, with MacroCommand, you can decide dynamically which commands you want to go into party command, so you have more flexibility using MacroCommands.
15. Adapter Pattern: Allow objects with incompatible interfaces to collaborate. 
```csharp
public interface IDuck
{
    void Quack();
    void Fly();
}

public class MallardDuck : IDuck
{
    public void Quack()
    {
        Console.WriteLine("Quack");
    }

    public void Fly()
    {
        Console.WriteLine("I am flying");
    }
}

public interface ITurkey
{
    void Gobble();
    void FlyShort();
}

public class TurkeyAdapter : ITurkey
{
    private readonly IDuck _duck;

    public TurkeyAdapter(IDuck duck)
    {
        _duck = duck;
    }

    public void Gobble()
    {
        _duck.Quack();
    }

    public void FlyShort()
    {
        _duck.Fly();
    }
}

class Program
{
    static void Main(string[] args)
    {
        IDuck mallardDuck = new MallardDuck();

        // Adapting MallardDuck to be a Turkey
        ITurkey turkeyAdapter = new TurkeyAdapter(mallardDuck);

        // Using the turkey interface
        turkeyAdapter.Gobble();
        turkeyAdapter.FlyShort();
    }
}

```
16. Decorator Patterns add new functionalities to an object without altering its structure. Adapter Pattern is used to allow two incompatible interfaces to work together. It doesn't add any new behavior. 
17. page 220
18. page 301+




# Head First Design Pattern

1. OOP Basics: inheritance, encapsulation(use private vars to store data, provide public methods), polymorphism, and abstraction(hide complex implementation details), ask chatGPT for examples
2. OO Principles:
    - Encapsulate what varies
    - Favor Composition over Inheritance
    - Program to interfaces, not implementation
    - Strive for loosely coupled designs between objects that interact
    - Class should be closed for modification but open for extension.
    - 
3. Strategy Pattern: Defining an interface, abstract class (Strategy) that represents a family of behaviors or methods(Algorithms). Concrete implementations of this interface represent specific behaviors, functions, or methods. By programming to the interface rather than to a specific implementation, you can switch out one behavior for another at runtime without changing the calling code.
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
When you have a group of behaviors would change depending on context(all ducks make sounds, but different sounds). Instead of putting methods in superclass and child inherited then overriding them one by one, some of the overrides would be the same(wood duck and steel duck both not making sounds). Strategy Pattern is good for solving this.
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
7. 
8. page 126
9. page 155




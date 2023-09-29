# Head First Design Pattern

1. OOP Basics: inheritance, encapsulation(use private vars to store data, provide public methods), polymorphism, and abstraction(hide complex implementation details), ask chatGPT for examples
2. OO Principles:
    - Encapsulate what varies
    - Favor Composition over Inheritance
    - Program to interfaces, not implementation
3. OO Patterns: Strategy Pattern,
4. Strategy Pattern: Defining an interface, abstract class (Strategy) that represents a family of behaviors or methods(Algorithms). Concrete implementations of this interface represent specific behaviors, functions, or methods. By programming to the interface rather than to a specific implementation, you can switch out one behavior for another at runtime without changing the calling code.
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
5. 

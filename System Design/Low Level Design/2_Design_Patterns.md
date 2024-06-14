# Design Patterns in Object-Oriented Programming (OOP)

Design patterns are reusable solutions to common problems that arise during software design. They provide a way to standardize and streamline the process of designing and communicating about software systems. In object-oriented programming (OOP), several design patterns are widely recognized and categorized into creational, structural, behavioral, architectural, and concurrency patterns.

## Creational Patterns

Creational patterns focus on the process of object creation, ensuring flexibility and reusability in object instantiation.

### Singleton Pattern

Ensures a class has only one instance and provides a global point of access to it.

### Factory Method Pattern

Defines an interface for creating objects, but lets subclasses decide which class to instantiate.

### Abstract Factory Pattern

Provides an interface for creating families of related or dependent objects without specifying their concrete classes.

## Structural Patterns

Structural patterns deal with the composition of classes and objects to form larger structures.

### Adapter Pattern

Allows objects with incompatible interfaces to work together by providing a wrapper with a compatible interface.

### Decorator Pattern

Allows behavior to be added to individual objects dynamically, without affecting the behavior of other objects from the same class.

### Facade Pattern

Provides a simplified interface to a complex subsystem, making it easier to use.

## Behavioral Patterns

Behavioral patterns focus on communication between objects, managing algorithms, and responsibilities.

### Observer Pattern

Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

### Strategy Pattern

Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

### Command Pattern

Encapsulates a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

## Architectural Patterns

Architectural patterns provide guidelines for organizing the structure and relationships of software components.

### MVC (Model-View-Controller) Pattern

Separates an application into three main components: Model (data), View (user interface), and Controller (business logic).

### Layered Pattern

Organizes the functionality of the system into distinct layers that interact through well-defined interfaces.

### Repository Pattern

Mediates between the domain and data mapping layers using a collection-like interface for accessing domain objects.

## Concurrency Patterns

Concurrency patterns deal with managing multiple threads and their interactions.

### Producer-Consumer Pattern

Involves splitting a task into a producer that generates work and a consumer that processes it, to handle multiple tasks efficiently.

### Read-Write Lock Pattern

Allows concurrent read access to a resource but requires exclusive access for write operations, optimizing performance in multi-threaded applications.

### Thread Pool Pattern

Manages a group of threads, improving performance and reducing overhead from thread creation.

# Strategy Pattern

The Strategy Pattern is a behavioral design pattern that defines a family of algorithms, encapsulates each one, and makes them interchangeable. This pattern allows the algorithm to vary independently from the clients that use it.

## Definition

The Strategy Pattern enables selecting an algorithm's behavior at runtime. Instead of implementing a single algorithm directly, the code receives run-time instructions as to which in a family of algorithms to use.

## Components

The Strategy Pattern typically involves the following components:

1. **Strategy Interface**: Defines a common interface for all supported algorithms.
2. **Concrete Strategies**: Implement the strategy interface with different algorithms.
3. **Context**: Maintains a reference to a strategy object and delegates the algorithm to the strategy interface.

## Benefits

- **Flexibility**: Allows the client to choose from a family of algorithms dynamically.
- **Reusability**: Encapsulates algorithms in separate classes, promoting code reuse.
- **Maintainability**: Simplifies the code by separating algorithm-specific behavior from the context.

## Example Implementation

Let's consider an example of a payment processing system where different payment methods can be used.

### 1. Strategy Interface

Define a common interface for all payment strategies:

```java
// PaymentStrategy.java
public interface PaymentStrategy {
    void pay(int amount);
}

```

### 2. Concrete Strategies

Implement the strategy interface with different payment methods:

```java
// CreditCardStrategy.java
public class CreditCardStrategy implements PaymentStrategy {
    private String name;
    private String cardNumber;
    private String cvv;
    private String dateOfExpiry;

    public CreditCardStrategy(String name, String cardNumber, String cvv, String dateOfExpiry) {
        this.name = name;
        this.cardNumber = cardNumber;
        this.cvv = cvv;
        this.dateOfExpiry = dateOfExpiry;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid with credit/debit card");
    }
}

// PayPalStrategy.java
public class PayPalStrategy implements PaymentStrategy {
    private String email;
    private String password;

    public PayPalStrategy(String email, String password) {
        this.email = email;
        this.password = password;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid using PayPal");
    }
}

// BitcoinStrategy.java
public class BitcoinStrategy implements PaymentStrategy {
    private String bitcoinAddress;

    public BitcoinStrategy(String bitcoinAddress) {
        this.bitcoinAddress = bitcoinAddress;
    }

    @Override
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Bitcoin.");
    }
}
```

### 3. Context

Maintain a reference to a strategy object and delegate the algorithm to the strategy interface:

```java
// ShoppingCart.java
import java.util.ArrayList;
import java.util.List;

public class ShoppingCart {
    private List<Item> items;

    public ShoppingCart() {
        this.items = new ArrayList<>();
    }

    public void addItem(Item item) {
        this.items.add(item);
    }

    public void removeItem(Item item) {
        this.items.remove(item);
    }

    public int calculateTotal() {
        return items.stream().mapToInt(Item::getPrice).sum();
    }

    public void pay(PaymentStrategy paymentMethod) {
        int amount = calculateTotal();
        paymentMethod.pay(amount);
    }
}
```

### Example Usage

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();

        cart.addItem(new Item("1234", 100));
        cart.addItem(new Item("5678", 200));

        PaymentStrategy creditCardStrategy = new CreditCardStrategy("John Doe", "1234567890123456", "123", "12/23");
        cart.pay(creditCardStrategy);

        PaymentStrategy payPalStrategy = new PayPalStrategy("john.doe@example.com", "password123");
        cart.pay(payPalStrategy);

        PaymentStrategy bitcoinStrategy = new BitcoinStrategy("1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa");
        cart.pay(bitcoinStrategy);
    }
}
```

In this example, the `ShoppingCart` class maintains a reference to a `PaymentStrategy` object and delegates the payment algorithm to the strategy interface. The client can choose from different payment methods (credit card, PayPal, Bitcoin) at runtime.
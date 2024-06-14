# SOLID Principles in OOPS

## What is SOLID?

SOLID is an acronym representing five fundamental principles of object-oriented design and programming, introduced by Robert C. Martin. These principles help create systems that are easier to maintain, extend, and understand. They are:

1. **S**ingle Responsibility Principle (SRP)
2. **O**pen/Closed Principle (OCP)
3. **L**iskov Substitution Principle (LSP)
4. **I**nterface Segregation Principle (ISP)
5. **D**ependency Inversion Principle (DIP)

### Why SOLID Principles are Needed

- **Understandability**: SOLID principles make code easier to read and understand by promoting clear, modular design.
- **Maintainability**: By ensuring that classes and methods have specific roles and responsibilities, it's easier to modify and extend the codebase without introducing bugs.
- **Flexibility**: Following SOLID principles makes it simpler to add new features to the system because changes are localized.
- **Reusability**: Components designed with SOLID principles can often be reused in different parts of the application or in different projects.
- **Testability**: Code adhering to SOLID principles is usually easier to test because dependencies are minimized and more clearly defined.
- **Scalability**: SOLID principles help in building scalable systems by reducing complexity and coupling between components.
- **Complexity**: Reduces complexity by breaking down the system into smaller, more manageable components.

## Single Responsibility Principle (SRP)

### Definition

The Single Responsibility Principle states that a class should have only one reason to change, meaning it should have only one job or responsibility.

### Need for SRP

- **Clarity**: A class with a single responsibility is easier to understand.
- **Maintenance**: Changes to one responsibility do not affect other responsibilities.
- **Decoupling**: Reduces the impact of changes and promotes reuse.

### Advantages of SRP

- **Simplicity**: Simplifies the design and implementation of a class.
- **Isolation**: Helps isolate and fix bugs since classes have distinct functionalities.
- **Flexibility**: Easier to refactor and adapt to new requirements.

### Disadvantages of SRP

- **Proliferation of Classes**: Can lead to a large number of small classes, which might be overwhelming.
- **Overhead**: Additional effort required to maintain a larger number of classes and manage their interactions.

### Example of SRP Violation

Let's consider a class :: - 

```java
//Marker Entity
class Marker{
  String name;
  String color;
  int price;
  int year;

  public Marker(String name, String color, int price, int year){
    this.name = name;
    this.color = color;
    this.price = price;
    this.year = year;
  }
}

// Invoice Entity

class Invoice{
  private Marker marker;
  private int quantity;

  public Invoice(Marker marker, int quantity){
    this.marker = marker;
    this.quantity = quantity;
  }

  public double calculateTotal(){
    double price = ((marker.price)*this.quantiy);
    return price;        //FIrst Responsibility :: it has responsibility of calculating total price
  }

  public void printInvoice(){
    System.out.println("Name: "+marker.name+" Color: "+marker.color+" Price: "+marker.price+" Quantity: "+this.quantity);
    //Second Responsibility :: it has responsibility of printing the invoice.
  }

  public void savetoDB(){
    //Third Responsibility :: it has responsibility of saving the invoice to DB.
  }
}
```

In the above example, the `Invoice` class has multiple responsibilities: calculating the total price, printing the invoice, and saving the invoice to the database. This violates the Single Responsibility Principle.Since SRP states that a class should have only one reason to change, meaning it should have only one job or responsibility.

### Refactored Example

```java

class Invoice{
  private Marker marker;
  private int quantity;

  public Invoice(Marker marker, int quantity){
    this.marker = marker;
    this.quantity = quantity;
  }

  public double calculateTotal(){
    double price = ((marker.price)*this.quantiy);
    return price;        //FIrst Responsibility :: it has responsibility of calculating total price
  }
}

class InvoicePrinter{

  private Invoice invoice;
  
  public InvoicePrinter(Invoice invoice){
    this.invoice = invoice;
  }



  public void printInvoice(Invoice invoice){
    System.out.println("Name: "+invoice.marker.name+" Color: "+invoice.marker.color+" Price: "+invoice.marker.price+" Quantity: "+invoice.quantity);
    //Second Responsibility :: it has responsibility of printing the invoice.
  }
}

class InvoiceDAO{
  private Invoice invoice;
  
  public InvoiceDAO(Invoice invoice){
    this.invoice = invoice;
  }
  public void savetoDB(Invoice invoice){
    //Third Responsibility :: it has responsibility of saving the invoice to DB.
  }
}
```

In the refactored example, the `Invoice` class now has only one responsibility: calculating the total price. The responsibilities of printing the invoice and saving it to the database have been moved to separate classes `InvoicePrinter` and `InvoiceDAO`, respectively.This adheres to the Single Responsibility Principle.

## Open/Closed Principle (OCP)

### Definition

The Open/Closed Principle states that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, the behavior of a module can be extended without modifying its source code.

### Need for OCP

- **Maintainability**: Allows for adding new features without modifying existing code.
- **Reusability**: Promotes reuse of existing code by extending its behavior.
- **Scalability**: Facilitates building scalable systems by adding new functionality through extensions.

### Advantages of OCP

- **Flexibility**: Allows for adding new features without breaking existing code.
- **Scalability**: Supports building systems that can be extended with new functionality.
- **Maintainability**: Reduces the risk of introducing bugs when adding new features.

### Disadvantages of OCP

- **Complexity**: Can lead to increased complexity due to the need for abstractions and extensions.
- **Overhead**: Additional effort required to design and implement abstractions for extensibility.


### Example of OCP Violation

Let's consider a class :: - 

```java
class Shape{
  String type;
  public Shape(String type){
    this.type = type;
  }

  public void draw(){
    if(this.type.equals("circle")){
      System.out.println("Drawing Circle");
    }else if(this.type.equals("rectangle")){
      System.out.println("Drawing Rectangle");
    }
  }
}
```

In the above example, the `Shape` class has a `draw` method that checks the type of the shape and performs different actions based on the type. If a new shape (e.g., triangle) needs to be added, the `draw` method must be modified to handle the new shape.This violates the Open/Closed Principle, as the class is not closed for modification.

Since the previous code is already tried and tested and it's live, there is a high chance that modifying it could introduce bugs.

### Refactored Example

```java
abstract class Shape{
  public abstract void draw();
}

class Circle extends Shape{
  @Override
  public void draw(){
    System.out.println("Drawing Circle");
  }
}

class Rectangle extends Shape{
  @Override
  public void draw(){
    System.out.println("Drawing Rectangle");
  }
}
```

In the refactored example, the `Shape` class has been converted into an abstract class with an abstract `draw` method. Concrete classes `Circle` and `Rectangle` extend the `Shape` class and provide their own implementations of the `draw` method. This adheres to the Open/Closed Principle, as new shapes can be added by creating new classes that extend the `Shape` class without modifying existing code.

## Liskov Substitution Principle (LSP)

### Definition

The Liskov Substitution Principle states that objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In other words, a subclass should be substitutable for its superclass.

A subclass should extend the capability of the parent class, not narrow it down.

If Class B is a subtype of Class A, then we should be able to replace objects of A with B without breaking the behavior of the program.

### Need for LSP

- **Correctness**: Ensures that substituting a subclass for its superclass does not break the program's correctness.
- **Flexibility**: Allows for polymorphic behavior by substituting objects of different subclasses.
- **Scalability**: Supports building systems that can be extended with new subclasses.

### Advantages of LSP

- **Polymorphism**: Enables polymorphic behavior by substituting objects of different subclasses.
- **Flexibility**: Allows for substituting objects of different subclasses without affecting the program's correctness.
- **Scalability**: Supports building systems that can be extended with new subclasses.

### Disadvantages of LSP

- **Complexity**: Can lead to increased complexity due to the need for ensuring substitutability.
- **Overhead**: Additional effort required to design and implement subclasses that adhere to the Liskov Substitution Principle.

### Example of LSP Violation

```java
interface Bike {
  void turnOnEngine();
  void accelerate();
}

class MotorCycle implements Bike {
  boolean isEngineOn;
  int speed;

  public void turnOnEngine() {
    this.isEngineOn = true;
  }

  public void accelerate() {
    this.speed = this.speed + 10;
  }
}

class Bicycle implements Bike {

  public void turnOnEngine() {
    throw new AssertionError("There is no engine to turn on");
  }

  public void accelerate() {
    this.speed = this.speed + 10;
  }
}
```
In the above example, the `MotorCycle` class doesn't narrow down any parent `Bike` behavior, whereas the `Bicycle` class narrows down the parent behavior by throwing an error when `turnOnEngine` is called. This means the `Bicycle` class cannot be substituted in place of the parent class where there is a need for an engine because it doesn't have one and if it is done it leads to the unexpected behaviour. A subclass having fewer functions than its superclass violates the LSP.

### Refactored Example

```java

interface Bike {
  void accelerate();
}

interface EngineBike extends Bike {
  void turnOnEngine();
}

class MotorCycle implements EngineBike {
  boolean isEngineOn;
  int speed;

  public void turnOnEngine() {
    this.isEngineOn = true;
  }

  public void accelerate() {
    this.speed = this.speed + 10;
  }
}

class Bicycle implements Bike {
  int speed;

  public void accelerate() {
    this.speed = this.speed + 10;
  }
}
```

In the refactored example, the `Bike` interface has been split into two interfaces: `Bike` and `EngineBike`. The `MotorCycle` class implements the `EngineBike` interface, which extends the `Bike` interface. The `Bicycle` class implements the `Bike` interface. This adheres to the Liskov Substitution Principle, as the `Bicycle` class can be substituted for the `Bike` interface without breaking the program's correctness.
 This ensures that subclasses do not narrow down the behavior of their parent class, adhering to the Liskov Substitution Principle.

## Interface Segregation Principle (ISP)

### Definition

The Interface Segregation Principle states that a client should not be forced to implement an interface that it doesn't use. In other words, classes should not be forced to depend on interfaces they do not use.

Interfaces shoule be such , the client should not implement unneccessary functions they do not need.

### Need for ISP

- **Modularity**: Promotes modularity by breaking down interfaces into smaller, more specific ones.
- **Flexibility**: Allows clients to implement only the interfaces they need, reducing unnecessary dependencies.
- **Scalability**: Supports building systems that can be extended with new interfaces.

### Advantages of ISP

- **Modularity**: Interfaces are broken down into smaller, more specific ones, promoting modularity.
- **Flexibility**: Clients can implement only the interfaces they need, reducing unnecessary dependencies.
- **Scalability**: Supports building systems that can be extended with new interfaces.

### Disadvantages of ISP

- **Complexity**: Can lead to increased complexity due to the need for more interfaces.
- **Overhead**: Additional effort required to design and implement more interfaces.


### Example of ISP Violation

```java
//Example 1 :: 
interface Worker {
  void work();
  void eat();
}

class Robot implements Worker {
  public void work() {
    System.out.println("Robot working");
  }

  public void eat() {
    // Robot doesn't eat
    throw new AssertionError("Robot cannot eat");
  }
}

class Human implements Worker {
  public void work() {
    System.out.println("Human working");
  }

  public void eat() {
    System.out.println("Human eating");
  }
}
```

```java
// Example 2

interface RestaurantEmployee{
  void washDishes;
  void serveCustomers;
  void cookFood;
}

class Waiter implements RestaurantEmployee{
  public void washDishes(){
    //Waiter doesn't wash dishes
  }

  public void serveCustomers(){
    System.out.println("Waiter serving customers");
  }

  public void cookFood(){
    //Waiter doesn't cook food
  }
}
```

In the above example, the `Worker` interface has two methods: `work` and `eat`. The `Robot` class implements the `Worker` interface but doesn't need the `eat` method. The `Human` class implements the `Worker` interface with both `work` and `eat` methods. This violates the Interface Segregation Principle, as the `Robot` class is forced to implement a method it doesn't need.

### Refactored Example

```java

interface Workable {
  void work();
}


interface Eatable {
  void eat();
}


class Robot implements Workable {
  public void work() {
    System.out.println("Robot working");
  }
}

class Human implements Workable, Eatable {
  public void work() {
    System.out.println("Human working");
  }

  public void eat() {
    System.out.println("Human eating");
  }
}
```

In the refactored example, the `Worker` interface has been split into two interfaces: `Workable` and `Eatable`. The `Robot` class implements the `Workable` interface, and the `Human` class implements both the `Workable` and `Eatable` interfaces. This adheres to the Interface Segregation Principle, as classes are not forced to implement methods they don't need.

```java
//Example 2

interface DishWasher{
  void washDishes;
}

interface FoodServer{
  void serveCustomers;
}

interface Cook{
  void cookFood;
}

class Waiter implements FoodServer{
  public void serveCustomers(){
    System.out.println("Waiter serving customers");
  }
}

class Chef implements Cook{
  public void cookFood(){
    System.out.println("Chef cooking food");
  }
}

class DishWasher implements DishWasher{
  public void washDishes(){
    System.out.println("Dishwasher washing dishes");
  }
}

// no any class is forced to implement any method which it doesn't need.
```

## Dependency Inversion Principle (DIP)

### Definition

The Dependency Inversion Principle states that high-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions.

In simpler terms, classes should depend on abstractions (interfaces) rather than concrete implementations.

### Need for DIP

- **Decoupling**: Reduces coupling between classes by depending on abstractions rather than concrete implementations.
- **Flexibility**: Allows for easier substitution of implementations without affecting the client code.
- **Scalability**: Supports building systems that can be extended with new implementations.

### Advantages of DIP

- **Decoupling**: Reduces coupling between classes by depending on abstractions.
- **Flexibility**: Allows for easier substitution of implementations without affecting the client code.
- **Scalability**: Supports building systems that can be extended with new implementations.

### Disadvantages of DIP

- **Complexity**: Can lead to increased complexity due to the need for abstractions and dependency injection.
- **Overhead**: Additional effort required to design and implement abstractions and dependency injection.

### Example of DIP Violation

```java
class LightBulb {
  public void turnOn() {
    System.out.println("LightBulb: Bulb turned on...");
  }

  public void turnOff() {
    System.out.println("LightBulb: Bulb turned off...");
  }
}

class Switch {
  private LightBulb bulb;

  public Switch() {
    this.bulb = new LightBulb(); // I only know LightBulb, i will have problem or their needs to be modification if you are not LightBulb // Tight coupling.
  }

  public void flipUp() {
    bulb.turnOn();
  }

  public void flipDown() {
    bulb.turnOff();
  }
}
```

In the above example, the `Switch` class directly depends on the `LightBulb` class, creating a tight coupling between the two classes. If a different type of bulb needs to be used, the `Switch` class must be modified to accommodate the new bulb. This violates the Dependency Inversion Principle, as the `Switch` class depends on a concrete implementation (`LightBulb`) rather than an abstraction.


### Refactored Example

```java
interface Switchable {
  void turnOn();
  void turnOff();
}

class LightBulb implements Switchable {
  public void turnOn() {
    System.out.println("LightBulb: Bulb turned on...");
  }

  public void turnOff() {
    System.out.println("LightBulb: Bulb turned off...");
  }
}

class Switch {
  private Switchable device;

  public Switch(Switchable device) {
    this.device = device; // I don't care whether you are LightBulb or not as long as you are Switchable
  }

  public void flipUp() {
    device.turnOn();
  }

  public void flipDown() {
    device.turnOff();
  }
}
```

In the refactored example, the `Switch` class depends on the `Switchable` interface rather than the `LightBulb` class directly. The `LightBulb` class implements the `Switchable` interface, and the `Switch` class is constructed with a `Switchable` device. This adheres to the Dependency Inversion Principle, as the `Switch` class depends on an abstraction (`Switchable`) rather than a concrete implementation (`LightBulb`).








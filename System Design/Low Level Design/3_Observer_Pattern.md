# Observer Pattern

The Observer Pattern is a behavioral design pattern that defines a one-to-many dependency between objects, so that when one object changes state, all its dependents are notified and updated automatically. It is used to establish communication between objects in a loosely coupled manner, allowing them to interact without being tightly coupled.
This pattern is widely used to implement distributed event-handling systems and is commonly seen in GUI toolkits, notification systems, and other event-driven software.


## Description

The Observer Pattern consists of two main components: the `Subject` and the `Observer`. The `Subject` maintains a list of observers and notifies them of state changes, while the `Observer` registers with the `Subject` to receive updates. When the `Subject` changes state, it notifies all registered observers, triggering them to update their state accordingly.

## Key Components

- **Subject:** The object being observed. It maintains a list of observers and provides methods to register, unregister, and notify observers of state changes. The object that holds the data and knows its observers. It provides methods to attach, detach, and notify observers.

- **Observer:** The object that observes the `Subject` and receives notifications of state changes. It defines an update method that is called by the `Subject` when its state changes. The object that is interested in the state of the subject and implements an update method to respond to changes.

- **ConcreteSubject**: The concrete implementation of the subject that holds the actual state of interest.

- **ConcreteObserver**: The concrete implementation of the observer that defines the behavior to be executed when notified of state changes.

## UML Diagram

The UML diagram below illustrates the structure of the Observer Pattern:

```sql
         +-----------------+         +-----------------+
         |     Subject     |<------->|    Observer     |
         +-----------------+         +-----------------+
         | -observers      |         | +update()       |
         +-----------------+         +-----------------+
         | +attach()       |         ^         ^
         | +detach()       |         |         |
         | +notify()       |         |         |
         +-----------------+         |         |
                |                    |         |
                v                    |         |
   +-----------------------+         |         |
   |    ConcreteSubject    |         |         |
   +-----------------------+         |         |
   | -state                |         |         |
   | +getState()           |         |         |
   | +setState()           |         |         |
   +-----------------------+         |         |
                                     |         |
                                     |         |
         +--------------------+      |         |
         | ConcreteObserver   |<-----+         |
         +--------------------+                |
         | -state             |<---------------+
         | +update()          |
         +--------------------+

```

## Implementation Steps

1. **Define Observer Interfaces:**
   - Create an interface for the `Observer` with a method to update its state based on changes in the `Subject`.
   ```java
   public interface Observer {
    void update(String state);
    }
   ```

2. **Define Subject Interface:**
   - Create an interface for the `Subject` with methods to attach, detach, and notify observers.
   ```java
   import java.util.ArrayList;
   import java.util.List;

   public abstract class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void attach(Observer observer) {
        observers.add(observer);
    }

    public void detach(Observer observer) {
        observers.remove(observer);
    }

    protected void notifyObservers(String state) {
        for (Observer observer : observers) {
            observer.update(state);
        }
    }
  } 
  ```

3. **Implement Concrete Subject:**
   - Create a concrete implementation of the `Subject` interface that holds the actual state of interest.

  ```java
   public class ConcreteSubject extends Subject {
    private String state;

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
        notifyObservers(state);
    }
  }
  ```

4. **Implement Concrete Observer:**
   - Create a concrete implementation of the `Observer` interface that defines the behavior to be executed when notified of state changes.

  ```java
   public class ConcreteObserver implements Observer {
    private String state;

    @Override
    public void update(String state) {
        this.state = state;
        System.out.println("Observer updated with state: " + state);
    }
  }
  ```

5. **Usage:**
   - Create instances of the `ConcreteSubject` and `ConcreteObserver` classes, attach the observer to the subject, and update the subject's state to trigger notifications.

  ```java
   public class Main {
    public static void main(String[] args) {
        ConcreteSubject subject = new ConcreteSubject();
        ConcreteObserver observer = new ConcreteObserver();

        subject.attach(observer);
        subject.setState("New State");
    }
  }
  ```

## When to Use

- When a change to one object requires changing others, and you don't know how many objects need to be changed.
- When an object should be able to notify other objects without making assumptions about who these objects are.
- Ideal for implementing distributed event-handling systems.

## Benefits

- **Loose Coupling:** The Observer Pattern decouples the subject and observers, allowing them to interact without being tightly coupled.
- **Scalability:** Observers can be added or removed dynamically, making it easy to scale the system.
- **Reusability:** The pattern promotes reusability by allowing multiple observers to monitor the same subject.
- **Event-Driven:** Enables event-driven communication between objects, making it suitable for event-handling systems.

## Drawbacks

- **Memory Leaks:** If observers are not properly detached from the subject, it can lead to memory leaks.
- **Ordering of Notifications:** The order in which observers are notified may not be guaranteed, leading to potential issues in certain scenarios.
- **Complexity:** The pattern can introduce complexity in managing the relationships between subjects and observers.

## Example

### Scenario: Weather Monitoring System

Consider a weather monitoring system where multiple displays need to be updated whenever the weather changes. The system consists of a `WeatherStation` as the subject and `Display` objects(such as Mobile , Laptop , T.V.) as observers. When the weather changes, all displays should be notified and updated with the new weather data.


### Key Componentes

- **WeatherStation:** The subject that holds the weather data and notifies displays of changes.
- **Display:** The observer that receives weather updates and displays the new data.Interface for displaying notifications
-**Observers:**  MobileNotification, LaptopNotification, TVNotification

### Implementation

1. **Subject Interface:**
```java
import java.util.ArrayList;
import java.util.List;

public interface Subject {
    void attach(Observer observer);
    void detach(Observer observer);
    void notifyObservers();
}

```
2. **Observer Interface:**
```java
public interface Observer {
    void update(float temperature, float humidity, float pressure);
}
```

3. **Concrete Subject:**
```java
import java.util.ArrayList;
import java.util.List;

public class WeatherData implements Subject {
    private List<Observer> observers;
    private float temperature;
    private float humidity;
    private float pressure;

    public WeatherData() {
        observers = new ArrayList<>();
    }

    @Override
    public void attach(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void detach(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(temperature, humidity, pressure);
        }
    }

    public void measurementsChanged() {
        notifyObservers();
    }

    public void setMeasurements(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        measurementsChanged();
    }
}
```

4. **Concrete Observer:**
 - MobileNotification
```java
public class MobileNotification implements Observer {
    private float temperature;
    private float humidity;
    private float pressure;

    @Override
    public void update(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        display();
    }

    public void display() {
        System.out.println("Mobile Notification: Temperature = " + temperature + "F, Humidity = " + humidity + "%, Pressure = " + pressure + " Pa");
    }
}
```
- LaptopNotification
```java
public class LaptopNotification implements Observer {
    private float temperature;
    private float humidity;
    private float pressure;

    @Override
    public void update(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        display();
    }

    public void display() {
        System.out.println("Laptop Notification: Temperature = " + temperature + "F, Humidity = " + humidity + "%, Pressure = " + pressure + " Pa");
    }
}
```
- TVNotification
```java
public class TVNotification implements Observer {
    private float temperature;
    private float humidity;
    private float pressure;

    @Override
    public void update(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        display();
    }

    public void display() {
        System.out.println("TV Notification: Temperature = " + temperature + "F, Humidity = " + humidity + "%, Pressure = " + pressure + " Pa");
    }
}
```

5. **Usage:**
```java
public class WeatherNotificationSystem {
    public static void main(String[] args) {
        WeatherData weatherData = new WeatherData();

        MobileNotification mobileNotification = new MobileNotification();
        LaptopNotification laptopNotification = new LaptopNotification();
        TVNotification tvNotification = new TVNotification();

        weatherData.attach(mobileNotification);
        weatherData.attach(laptopNotification);
        weatherData.attach(tvNotification);

        weatherData.setMeasurements(80, 65, 1013);
        weatherData.setMeasurements(82, 70, 1012);
        weatherData.setMeasurements(78, 90, 1011);
    }
}
```










Using **constructor injection with an interface** is a best practice because the class depends on an **abstraction (interface)** instead of a concrete implementation. This follows the Dependency Inversion Principle **(DIP)**.

**Create an Interface**

```java
interface Engine {
    void start();
}
```

**Create implementations**

```java
class PetrolEngine implements Engine {

    @Override
    public void start() {
        System.out.println("Petrol engine started");
    }
}
```

```java
class ElectricEngine implements Engine {

    @Override
    public void start() {
        System.out.println("Electric engine started");
    }
}
```

**Inject the interface through the constructor**

```java
class Car {

    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is moving");
    }
}
```

Notice that `Car` doesn't know whether it's using a `PetrolEngine` or an `ElectricEngine`. It only knows that it has an `Engine`.

**Use different implementations**

```java
public class Main {

    public static void main(String[] args) {

        Engine petrol = new PetrolEngine();
        Car car1 = new Car(petrol);
        car1.drive();

        Car car2 = new Car(new ElectricEngine());
        car2.drive();
    }
}
```

> [!Output:]
> Petrol engine started
> Car is moving
>
> Electric engine started
> Car is moving

**_Why inject an interface instead of a class?_**

- _Loose coupling:_ `Car` depends on the `Engine` interface, not a specific engine type.
- _Easy to replace implementations:_ Switch from `PetrolEngine` to `ElectricEngine` without changing `Car`.
- _Easy testing:_ Inject a fake or mock implementation during unit tests.
- _Better design:_ Your code follows the Dependency Inversion Principle.

---

> [!Open/Closed Principle (OCP):]
>
> 1. It is one of the the five SOLID principles of object oriented design
> 2. Software entities (Classes, methods, modules) should be open for extension but closed for modification
>
> This means:
>
> > a. Open for extension: You should be able to add new functionality.
> > b. Closed for modification: You should not have to change existing, working code

Note:

- If we want to add new functionality then add a separate class that implements its desire interfaces

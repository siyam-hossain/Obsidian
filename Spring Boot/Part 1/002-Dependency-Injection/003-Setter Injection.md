**Setter Injection** is a type of Dependency Injection where the dependency is provided through a **setter method** after the object has been created.

**Create an interface**

```java
interface Engine {
    void start();
}
```

**Implement the interface**

```java
class PetrolEngine implements Engine {

    @Override
    public void start() {
        System.out.println("Petrol engine started");
    }
}
```

**Use Setter Injection**

```java
class Car {

    private Engine engine;

    // Setter Injection
    public void setEngine(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is moving");
    }
}
```

**Inject the dependency**

```java
public class Main {

    public static void main(String[] args) {

        Engine engine = new PetrolEngine();

        Car car = new Car();      // Object created first
        car.setEngine(engine);    // Dependency injected later

        car.drive();
    }
}
```

---

**Constructor Injection vs Setter Injection**

| Constructor Injection                    | Setter Injection                             |
| ---------------------------------------- | -------------------------------------------- |
| Dependency is passed in the constructor  | Dependency is passed through a setter method |
| Required dependencies                    | Optional dependencies                        |
| Supports `final` fields                  | Cannot use `final` fields                    |
| Object is fully initialized when created | Object may exist without its dependency      |
| Preferred in Spring                      | Used mainly for optional dependencies        |

---

**When to Use Setter Injection**

Use setter injection when:

- The dependency is **optional**.
- You may want to **change the dependency after object creation**.
- You don't want to force every object to have that dependency.

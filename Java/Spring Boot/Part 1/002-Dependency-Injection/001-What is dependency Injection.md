**Dependency Injection (DI)** is a design pattern in Java where an object receives the objects it depends on from the outside instead of creating them itself.

**Without Dependency Injection**
Here, `Car` creates its own `Engine`:

```java
class Engine {
	void start() {
		System.out.println("Engine started");
	}
}
```

```java
class Car {
    private Engine engine = new Engine(); // Car creates Engine
    void drive() {
		    engine.start();
		    System.out.println("Car is moving");
	    }
	}
```

> [!problem]
> `Car` is tightly coupled to `Engine`.
> Harder to replace `Engine` with a different implementation or a mock for testing.

---

**With Dependency Injection**
The `Engine` is provided from outside:

```java
class Engine {
	void start() {
		System.out.println("Engine started");
	}
}
```

```java
class Car {
	private Engine engine;

	// Dependency is injected through the constructor
	public Car(Engine engine) {
			this.engine = engine;
		}

	void drive() {
			engine.start();
			System.out.println("Car is moving");
		}
}
```

```java
public class Main {
	public static void main(String[] args) {
		Engine engine = new Engine();
		Car car = new Car(engine); // Inject dependency
		car.drive();
	}
}
```

Now `Car` doesn't know how to create an `Engine`; it only knows how to use one.

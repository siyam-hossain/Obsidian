# Advanced principles of Object Oriented Design (OOD)

ODD are guidelines that help developers design software that is **maintainable, scalable, reusable, and easy to modify**.

### SOLID Principle

| S   | Single responsibility principle |
| --- | ------------------------------- |
| O   | Open/closed principle           |
| L   | Liskov substitution principle   |
| I   | Interface segregation principle |
| D   | Dependency inversion principle  |

### Single Responsibility principle (SRP)

**Definition**
The Single Responsibility Principle (SRP) is the first principle of the SOLID principles of ODD. It sates:

> A class should have only one responsibility, or one reason to change.

This means a class should perform only one specific task. If a class has multiple responsibilities, changes in one responsibility may affect the others, making the code harder to maintain.

**Characteristics of SRP**

1. One responsibility per class: each class should focus on a single job.
2. One reason to change: A class should change only when its specific responsibility changes.
3. High cohesion: The methods and variables in a class are closely related to one purpose.
4. Low coupling: Classes depend less on each other, making them easier to modify.
5. Better maintainability: Small, focused classes are easier to understand and update.

**Advantages**

1. Improves code readability.
2. Makes code easier to maintain.
3. Simplifies testing because each class has a single purpose.
4. Encourages code reuse.
5. Reduces the impact of changes.
6. Makes debugging easier.

**Disadvantages**

1. Increases the number of classes in a project
2. May make the project structure more complex.
3. Requires more planning during design.
4. Can result in additional communication between classes

##### Code Example

**Without SRP**

```java
class Employee {

    public void calculateSalary() {
        System.out.println("Calculating salary...");
    }

    public void saveToDatabase() {
        System.out.println("Saving employee to database...");
    }

    public void generateReport() {
        System.out.println("Generating employee report...");
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee();

        emp.calculateSalary();
        emp.saveToDatabase();
        emp.generateReport();
    }
}
```

**Problem**
The `Employee` class has three responsibilities:

- Salary calculation
- Database operations
- Report generation
  If any of these features change, the `Employee` class must also change, violating SRP.

---

**With SRP**

```java
class Employee {
    private String name;

    public Employee(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

```java
class SalaryCalculator {
    public void calculateSalary(Employee employee) {
        System.out.println("Calculating salary for " + employee.getName());
    }
}
```

```java
class EmployeeRepository {
    public void save(Employee employee) {
        System.out.println("Saving " + employee.getName() + " to database");
    }
}
```

```java
class ReportGenerator {
    public void generate(Employee employee) {
        System.out.println("Generating report for " + employee.getName());
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee("John");

        SalaryCalculator salary = new SalaryCalculator();
        EmployeeRepository repository = new EmployeeRepository();
        ReportGenerator report = new ReportGenerator();

        salary.calculateSalary(emp);
        repository.save(emp);
        report.generate(emp);
    }
}
```

**Explanation**

- `Employee` stores employee data.
- `SalaryCalculator` handles salary calculation.
- `EmployeeRepository` manages database operations.
- `ReportGenerator` creates reports.
  Each class has only one responsibility, so the design follows the Single Responsibility Principle.

---

### Open/Closed Principle (OCP)

**Definition**
The OCP is the second principle of the SOLID principles of OOD. It states:

> Software entities (classes, methods, modules, etc.) should be open for extension but closed for modification.

This means you should be able to add new functionality by creating new classes or extending existing ones, without changing the existing, tested code.

**Characteristics of OCP**

1. Open for extension: New features can be added by extending existing classes.
2. Closed for modification: Existing source code should not need to be changed.
3. Uses abstraction: Achieved through interfaces or abstract classes.
4. Promotes polymorphism: Different implementations can be used interchangeably.
5. Reduces risk: Existing code remains stable and less likely to introduce bugs.

**Advantages**

- Improves maintainability.
- Makes code easier to extend.
- Reduces the risk of breaking existing functionality.
- Encourages reusable and flexible designs.
- Supports scalability as new requirements arise.

**Disadvantages**

- May increase the number of classes and interfaces.
- Initial design can be more complex.
- Can lead to over-engineering if applied unnecessarily.

##### Code Example

**Without OCP**

```java
class AreaCalculator {

    double calculate(Object shape) {

        if (shape instanceof Circle) {
            Circle circle = (Circle) shape;
            return Math.PI * circle.radius * circle.radius;
        }
        else if (shape instanceof Square) {
            Square square = (Square) shape;
            return square.side * square.side;
        }

        return 0;
    }
}
```

**Why is this bad?**

- Every time a new shape is added, you must modify the `calculate()` method.
- The class keeps growing with more `if-else` conditions.
- Existing code changes whenever new functionality is added.
- This violates the open/closed principle, because the class is not closed for modification.

---

**With OCP**

Create an interface

```java
interface Shape {
    double area();
}
```

Implement the interface

```java
class Circle implements Shape {

    double radius;

    Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}
```

```java
class Square implements Shape {

    double side;

    Square(double side) {
        this.side = side;
    }

    @Override
    public double area() {
        return side * side;
    }
}
```

Area Calculator

```java
class AreaCalculator {

    double calculate(Shape shape) {
        return shape.area();
    }
}
```

Main Class

```java
public class Main {

    public static void main(String[] args) {

        AreaCalculator calculator = new AreaCalculator();

        Shape circle = new Circle(5);
        Shape square = new Square(4);

        System.out.println("Circle Area : " +
                calculator.calculate(circle));

        System.out.println("Square Area : " +
                calculator.calculate(square));
    }
}
```

Notice that `AreaCalculator` does not change at all. Only a new class is added

---

### Liskov Substitution Principle (LSP)

**Definition**

> Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness or expected behavior of the program.

In simple words:

> A child class should behave like its parent class. Replacing the parent with the child should not produce unexpected results.

**Without LSP (Violates LSP)**

```java
class Green {

    public void getColor() {
        System.out.println("Green");
    }
}

class Blue extends Green {

    @Override
    public void getColor() {
        System.out.println("Blue");
    }
}

public class Main {

    public static void main(String[] args) {

        // Violates LSP
        Green green = new Blue();
        green.getColor();

        // Output: Blue
    }
}
```

**Problem**

Suppose the object type is **Green**.

```java
Green green = new Blue();
green.getColor();
```

Expected Output:

```
Green
```

Actual Output:

```
Blue
```

**Why does this violate LSP?**

- A `Green` object is expected to behave like **Green**.
- But replacing it with a `Blue` object changes the expected behavior.
- The child class (`Blue`) does **not** preserve the contract of the parent (`Green`).
- Therefore, this inheritance relationship violates the Liskov Substitution Principle.

---

**With LSP (Correct Design)**

Instead of inheritance, use an interface because Green is not a specialized form of Blue, and Blue is not a specialized form of Green.

Step 1: Interface

```java
interface IColor {
    void getColor();
}
```

Step 2: Green Class

```java
class Green implements IColor {

    @Override
    public void getColor() {
        System.out.println("Green");
    }
}
```

Step 3: Blue Class

```java
class Blue implements IColor {

    @Override
    public void getColor() {
        System.out.println("Blue");
    }
}
```

Step 4: Main Class

```java
public class Main {

    public static void main(String[] args) {

        IColor color;

        color = new Green();
        color.getColor();     // Output: Green

        color = new Blue();
        color.getColor();     // Output: Blue
    }
}
```

Output

```
Green
Blue
```

**Why this follows LSP**

- `IColor` defines a common contract: `getColor()`.
- `Green` and `Blue` both implement the same contract.
- They are alternative implementations, not parent-child replacements.
- No class changes another class's expected behavior.
- The program behaves correctly regardless of which implementation is used.

**Characteristics of LSP**

- A subclass should be completely replaceable for its superclass.
- The child class should not change the expected behavior of the parent.
- Supports proper inheritance and polymorphism.
- Prevents unexpected runtime behavior.
- Promotes reliable and maintainable code.
  **Advantages**
- Improves code reliability.
- Encourages correct inheritance.
- Supports polymorphism.
- Easier to maintain and extend.
- Reduces runtime errors.

**Disadvantages**

- Requires careful class hierarchy design.
- Incorrect inheritance can easily violate LSP.
- Sometimes composition or interfaces are better than inheritance.

---

### Interface Segregation Principle (ISP) in Java

**Definition**
The Interface Segregation Principle (ISP) is the fourth principle of the SOLID principles of object-oriented design. It states:

**Clients should not be forced to depend on interfaces they do not use.**

In simple words:

> **Instead of one large interface, create multiple small, specific interfaces so that implementing classes only need to implement the methods they actually need.**

**Characteristics of ISP**

1. Create small and focused interfaces.
2. A class should implement only the methods it requires.
3. Avoid "fat" or "bloated" interfaces.
4. Promotes loose coupling.
5. Improves flexibility and maintainability.

**Advantages**

- Reduces unnecessary dependencies.
- Improves code readability.
- Easier to maintain and extend.
- Encourages reusable interfaces.
- Prevents empty or unsupported method implementations.

**Disadvantages**

- May increase the number of interfaces.
- Can make the design slightly more complex.
- Requires careful interface design.

**Without ISP (Violates ISP)**
Suppose we have a common interface for all workers.

```java
interface Worker {

    void work();

    void eat();
}
```

Human Worker

```java
class HumanWorker implements Worker {

    @Override
    public void work() {
        System.out.println("Human is working");
    }

    @Override
    public void eat() {
        System.out.println("Human is eating");
    }
}
```

Robot Worker

```java
class RobotWorker implements Worker {

    @Override
    public void work() {
        System.out.println("Robot is working");
    }

    @Override
    public void eat() {
        throw new UnsupportedOperationException("Robot doesn't eat");
    }
}
```

Main Class

```java
public class Main {

    public static void main(String[] args) {

        Worker human = new HumanWorker();
        human.work();
        human.eat();

        Worker robot = new RobotWorker();
        robot.work();
        robot.eat();   // Runtime Exception
    }
}
```

Problem

- `RobotWorker` is forced to implement `eat()`.
- Robots do **not** eat.
- The method throws an exception or remains empty.
- This **violates the Interface Segregation Principle** because the class depends on a method it does not need.

**With ISP (Follows ISP)**
Split the large interface into smaller interfaces.

Step 1: Work Interface

```java
interface Workable {
    void work();
}
```

Step 2: Eat Interface

```java
interface Eatable {
    void eat();
}
```

Step 3: Human Worker

```java
class HumanWorker implements Workable, Eatable {

    @Override
    public void work() {
        System.out.println("Human is working");
    }

    @Override
    public void eat() {
        System.out.println("Human is eating");
    }
}
```

Step 4: Robot Worker

```java
class RobotWorker implements Workable {

    @Override
    public void work() {
        System.out.println("Robot is working");
    }
}
```

Step 5: Main Class

```java
public class Main {

    public static void main(String[] args) {

        Workable human = new HumanWorker();
        human.work();

        Eatable person = new HumanWorker();
        person.eat();

        Workable robot = new RobotWorker();
        robot.work();
    }
}
```

Output

```text
Human is working
Human is eating
Robot is working
```

Why this follows ISP

- `Workable` contains only work-related behavior.
- `Eatable` contains only eating-related behavior.
- `HumanWorker` implements both because it can work and eat.
- `RobotWorker` implements only `Workable` because robots don't eat.
- No class is forced to implement unnecessary methods.

| Aspect                | Description                                                                                                  |
| --------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Definition**        | Clients should not be forced to depend on methods they do not use.                                           |
| **Characteristics**   | Small interfaces, focused responsibilities, loose coupling, improved maintainability.                        |
| **Advantages**        | Better flexibility, readability, reusability, and fewer unnecessary dependencies.                            |
| **Disadvantages**     | More interfaces to manage and slightly increased design complexity.                                          |
| **Violation Example** | `RobotWorker` is forced to implement `eat()` even though robots don't eat.                                   |
| **Correct Example**   | Split `Worker` into `Workable` and `Eatable`, allowing each class to implement only the interfaces it needs. |

### Dependency Inversion Principle (DIP) in Java

**Definition**
The Dependency Inversion Principle (DIP) is the fifth and final principle of the **SOLID** principles. It emphasizes **decoupling** and **abstraction**.

It states:

> **High-level modules should not depend on low-level modules. Both should depend on abstractions (interfaces or abstract classes).**
> **Abstractions should not depend on details. Details should depend on abstractions.**

**Simple Meaning**
Instead of a class depending directly on another concrete class, it should depend on an **interface**. This makes the code flexible and easier to extend.

**Characteristics of DIP**

1. High-level modules depend on abstractions.
2. Low-level modules also depend on abstractions.
3. Interfaces separate implementation from usage.
4. Promotes loose coupling.
5. Makes applications easier to extend and maintain.

**Advantages**

- Reduces coupling between classes.
- Easier to maintain.
- Easy to replace implementations.
- Improves flexibility and scalability.
- Simplifies unit testing (using mock objects).

**Disadvantages**

- More interfaces and classes.
- Slightly more complex design.
- May be unnecessary for very small projects.

**Without DIP (Violates DIP)**
Suppose a `Notification` class sends emails.

Email Service

```java
class EmailService {

    public void sendMessage(String message) {
        System.out.println("Email Sent: " + message);
    }
}
```

Notification Class

```java
class Notification {

    private EmailService emailService = new EmailService();

    public void notifyUser(String message) {
        emailService.sendMessage(message);
    }
}
```

Main Class

```java
public class Main {

    public static void main(String[] args) {

        Notification notification = new Notification();
        notification.notifyUser("Welcome to our application!");
    }
}
```

Problem

- `Notification` directly depends on `EmailService`.
- If later you want to use `SMSService` or `WhatsAppService`, you must modify the `Notification` class.
- This creates **high coupling**.
- It violates the Dependency Inversion Principle.

**With DIP (Follows DIP)**

Step 1: Create an Interface

```java
interface MessageService {
    void sendMessage(String message);
}
```

Step 2: Email Implementation

```java
class EmailService implements MessageService {

    @Override
    public void sendMessage(String message) {
        System.out.println("Email Sent: " + message);
    }
}
```

Step 3: SMS Implementation

```java
class SMSService implements MessageService {

    @Override
    public void sendMessage(String message) {
        System.out.println("SMS Sent: " + message);
    }
}
```

Step 4: Notification Class

```java
class Notification {

    private MessageService messageService;

    public Notification(MessageService messageService) {
        this.messageService = messageService;
    }

    public void notifyUser(String message) {
        messageService.sendMessage(message);
    }
}
```

Step 5: Main Class

```java
public class Main {

    public static void main(String[] args) {

        MessageService email = new EmailService();
        Notification notification1 = new Notification(email);
        notification1.notifyUser("Welcome!");

        MessageService sms = new SMSService();
        Notification notification2 = new Notification(sms);
        notification2.notifyUser("OTP: 123456");
    }
}
```

Output

```text
Email Sent: Welcome!
SMS Sent: OTP: 123456
```

Why this follows DIP

- `Notification` depends on the **`MessageService` interface**, not on `EmailService` or `SMSService`.
- `EmailService` and `SMSService` are different implementations of the same abstraction.
- New services (e.g., `WhatsAppService`, `PushNotificationService`) can be added **without modifying** the `Notification` class.
- This creates **low coupling**, making the code **flexible, maintainable, and extensible**.

| Aspect                | Description                                                                                                                                                                        |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Definition**        | High-level modules should not depend on low-level modules. Both should depend on abstractions.                                                                                     |
| **Characteristics**   | Uses interfaces, promotes abstraction, loose coupling, flexible design.                                                                                                            |
| **Advantages**        | Easier maintenance, scalability, testing, flexibility, and code reuse.                                                                                                             |
| **Disadvantages**     | More interfaces/classes and slightly increased design complexity.                                                                                                                  |
| **Violation Example** | `Notification` directly depends on `EmailService`. Adding `SMSService` requires modifying `Notification`.                                                                          |
| **Correct Example**   | `Notification` depends on the `MessageService` interface. Different implementations (`EmailService`, `SMSService`, `WhatsAppService`) can be used without changing `Notification`. |

## Comparison table

| Criteria                           | **SRP**                      | **OCP**                           | **LSP**                 | **ISP**                   | **DIP**                                         |
| ---------------------------------- | ---------------------------- | --------------------------------- | ----------------------- | ------------------------- | ----------------------------------------------- |
| **Main Goal**                      | One responsibility per class | Extend without modifying          | Correct inheritance     | Small, focused interfaces | Depend on abstractions                          |
| **Best Used When**                 | A class has multiple jobs    | New features are added frequently | Using inheritance       | Large interfaces exist    | High-level modules use multiple implementations |
| **File Size**                      | ⭐ Small                     | ⭐⭐⭐ Medium                     | ⭐⭐ Medium             | ⭐⭐⭐ Medium             | ⭐⭐⭐⭐ Large                                  |
| **Code Complexity**                | ⭐ Lowest                    | ⭐⭐⭐ Medium                     | ⭐⭐ Medium             | ⭐⭐⭐ Medium             | ⭐⭐⭐⭐ Highest                                |
| **Number of Classes**              | Few                          | More                              | Moderate                | More interfaces           | Most classes/interfaces                         |
| **Learning Difficulty**            | ⭐ Easy                      | ⭐⭐ Easy-Medium                  | ⭐⭐ Medium             | ⭐⭐⭐ Medium             | ⭐⭐⭐⭐ Hard                                   |
| **Maintainability**                | ⭐⭐⭐⭐ High                | ⭐⭐⭐⭐⭐ Very High              | ⭐⭐⭐⭐ High           | ⭐⭐⭐⭐ High             | ⭐⭐⭐⭐⭐ Excellent                            |
| **Scalability**                    | ⭐⭐⭐ Good                  | ⭐⭐⭐⭐⭐ Excellent              | ⭐⭐⭐ Good             | ⭐⭐⭐⭐ High             | ⭐⭐⭐⭐⭐ Excellent                            |
| **Flexibility**                    | ⭐⭐⭐ Medium                | ⭐⭐⭐⭐⭐ Excellent              | ⭐⭐⭐ Medium           | ⭐⭐⭐⭐ High             | ⭐⭐⭐⭐⭐ Excellent                            |
| **Coupling Reduction**             | ⭐⭐ Low                     | ⭐⭐⭐ Medium                     | ⭐⭐⭐ Medium           | ⭐⭐⭐⭐ High             | ⭐⭐⭐⭐⭐ Highest                              |
| **Reusability**                    | ⭐⭐⭐ Good                  | ⭐⭐⭐⭐⭐ Excellent              | ⭐⭐⭐ Good             | ⭐⭐⭐⭐ High             | ⭐⭐⭐⭐⭐ Excellent                            |
| **Testing**                        | ⭐⭐⭐⭐ Easy                | ⭐⭐⭐⭐ Easy                     | ⭐⭐⭐ Medium           | ⭐⭐⭐⭐ Easy             | ⭐⭐⭐⭐⭐ Very Easy (Mocking)                  |
| **Performance Impact**             | Very Low                     | Very Low                          | Very Low                | Very Low                  | Slightly Higher (due to abstractions)           |
| **Recommended for Small Projects** | ✅ Yes                       | ⚠️ If needed                      | ⚠️ If using inheritance | ❌ Usually unnecessary    | ❌ Usually overkill                             |
| **Recommended for Large Projects** | ✅ Yes                       | ✅ Yes                            | ✅ Yes                  | ✅ Yes                    | ✅ Yes                                          |

### If your priority is...

| Goal                                               | Recommended Principle                   |
| -------------------------------------------------- | --------------------------------------- |
| **Minimum file size**                              | **SRP**                                 |
| **Minimum complexity**                             | **SRP**                                 |
| **Fast development**                               | **SRP**                                 |
| **Fewest classes**                                 | **SRP**                                 |
| **Easy debugging**                                 | **SRP**                                 |
| **Adding new features frequently**                 | **OCP**                                 |
| **Using inheritance correctly**                    | **LSP**                                 |
| **Removing unnecessary methods from interfaces**   | **ISP**                                 |
| **Reducing coupling as much as possible**          | **DIP**                                 |
| **Maximum flexibility**                            | **DIP + OCP**                           |
| **Enterprise applications (Spring Boot, Java EE)** | **DIP + OCP + SRP**                     |
| **Best maintainability**                           | **SRP + OCP + ISP + DIP**               |
| **Best overall architecture**                      | **Apply all SOLID principles together** |

## Which principle should you choose?

| Project Type                         | Recommended SOLID Principles |
| ------------------------------------ | ---------------------------- |
| **Small Java program (100–500 LOC)** | SRP                          |
| **University assignment**            | SRP + OCP                    |
| **Desktop application**              | SRP + OCP + LSP              |
| **REST API / Spring Boot**           | SRP + OCP + DIP              |
| **Large enterprise application**     | All SOLID principles         |
| **Library or Framework**             | OCP + DIP + ISP              |

### Overall ranking

| Rank | Principle | Importance                                   |
| ---- | --------- | -------------------------------------------- |
| 🥇 1 | **SRP**   | Foundation of clean code                     |
| 🥈 2 | **OCP**   | Makes software extensible                    |
| 🥉 3 | **DIP**   | Reduces coupling and improves flexibility    |
| 4    | **ISP**   | Keeps interfaces clean and focused           |
| 5    | **LSP**   | Ensures correct inheritance and polymorphism |

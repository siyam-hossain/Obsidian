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
4. Requires more planning during design.
5. Can result in additional communication between classes

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

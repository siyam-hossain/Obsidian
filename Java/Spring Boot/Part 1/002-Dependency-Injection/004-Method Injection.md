**Method Injection** is a type of Dependency Injection where a dependency is passed **as a parameter to a method** instead of through the constructor or a setter.

Unlike constructor injection (dependency is available for the object's lifetime) and setter injection (dependency is stored in a field), method injection provides the dependency **only when the method is called**.

**Create an interface**

```java
interface MessageService {
    void send(String message);
}
```

**Implement the interface**

```java
class EmailService implements MessageService {
	@Override
	public void send(String message) {
		System.out.println("Email: " + message);
	}
}
```

```java
class SmsService implements MessageService {
	@Override
	public void send(String message) {
		System.out.println("SMS: " + message);
	}
}
```

**Inject the dependency through a method**

```java
class Notification {

    public void notifyUser(MessageService service, String message) {
        service.send(message);
    }
}
```

**Use it**

```java
public class Main {

    public static void main(String[] args) {

        Notification notification = new Notification();

        notification.notifyUser(new EmailService(), "Welcome!");
        notification.notifyUser(new SmsService(), "Your OTP is 1234");
    }
}
```

> [!Output:]
>
> > Email: Welcome!
> > SMS: Your OTP is 1234

---

**Why Use Method Injection?**
Suppose a class doesn't always need the same dependency. Instead of storing it as a field, you pass it only when needed.

For example: `Printer` is only needed while generating the report.

---

**Comparison**

| Injection Type        | When dependency is provided      | Stored in object?           |
| --------------------- | -------------------------------- | --------------------------- |
| Constructor Injection | During object creation           | ✅ Yes                      |
| Setter Injection      | After object creation            | ✅ Yes                      |
| Method Injection      | When a specific method is called | ❌ No (unless you store it) |

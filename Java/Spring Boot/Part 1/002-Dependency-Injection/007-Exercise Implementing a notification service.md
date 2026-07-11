Your task is to design a flexible notification system for an application. The system should be able to send notifications through different channels, such as email and SMS. You need to implement a solution tat allows swapping the notification methods without changing the core application logic.

This is a simulation, so no actual emails or SMS message will be sent this exercise focuses purely on the design and usage of Spring's IoC (Inversion of Control) container to manage dependencies.

_Class Diagram Overview_
Before diving into the implementation, here is a class diagram that represents the final design of your solution. It shows how the various components, such as the notificationService interface, its implementations (EmailNotificationService and SMSNotificationService), and the NotificationManager interact with each other.

![[007-UML diagram.png]]

---

The goal is to **design the application so you can switch between Email and SMS without modifying the main application code**. Spring IoC (Inversion of Control) handles which implementation is used.

### 1. `NotificationService` (Interface)

```java
public interface NotificationService {
    void send(String message);
}
```

- Defines a common contract.
- Any notification type (Email, SMS, Push, etc.) must implement `send()`.

---

### 2. `EmailNotificationService`

```java
@Service("email")
@Primary
public class EmailNotificationService implements NotificationService
```

- Implements `NotificationService`.
- `@Service` tells Spring to create an object (bean).
- `@Primary` tells Spring:
    - "If there are multiple implementations, use this one by `default`."

```java
public void send(String message) {
    System.out.println("Sending email: " + message);
}
```

---

### 3. `SMSNotificationService`

```java
@Service
public class SMSNotificationService implements NotificationService
```

Another implementation of the same interface.

```java
public void send(String message) {
    System.out.println("Sending SMS: " + message);
}
```

Now Spring has **two beans** of type `NotificationService`:

- `EmailNotificationService`
- `SMSNotificationService`

Without `@Primary` (or `@Qualifier`), Spring wouldn't know which one to inject.

---

### 4. `NotificationManager`

```java
@Service
public class NotificationManager {
```

This class **uses** a notification service.

```java
private final NotificationService notificationService;
```

Notice it depends on the **interface**, not Email or SMS directly.

Constructor Injection:

```java
public NotificationManager(NotificationService notificationService) {
    this.notificationService = notificationService;
}
```

Spring automatically injects the implementation. Because `EmailNotificationService` is `@Primary`, it injects that one.

```java
public void sendNotification(String message){
    notificationService.send(message);
}
```

The manager doesn't know whether it's sending an email or SMS. It simply calls `send()`.

This is **dependency injection**.

---

### 5. Main Class

```java
ApplicationContext context = SpringApplication.run(...);
```

Starts Spring and creates all beans.

```java
var manager = context.getBean(NotificationManager.class);
```

Gets the `NotificationManager` bean.

```java
manager.sendNotification("This is a test");
```

Calls:

```
NotificationManager
        ↓
NotificationService
        ↓
EmailNotificationService (because of @Primary)
```

Output:

```
Sending email: This is a test
```

---

## Why use IoC?

Without Spring:

```java
NotificationService service = new EmailNotificationService();
NotificationManager manager = new NotificationManager(service);
```

To switch to SMS:

```java
NotificationService service = new SMSNotificationService();
```

You must change the code.

With Spring:

- The application depends only on `NotificationService`.
- Spring decides which implementation to inject.
- You can switch implementations using `@Primary`, `@Qualifier`, or configuration, without changing `NotificationManager`.

---

### Flow

```
Main
  ↓
Gets NotificationManager bean
  ↓
NotificationManager
  ↓
NotificationService (interface)
  ↓
EmailNotificationService (@Primary)
or
SMSNotificationService
```

This is the key idea of Spring IoC: **your classes depend on abstractions (interfaces), and Spring injects the appropriate implementation automatically.**

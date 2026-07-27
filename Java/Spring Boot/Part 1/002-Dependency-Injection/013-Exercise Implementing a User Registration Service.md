In this exercise, you will design an implement a User Registration Service that allows user to register by providing their name, email, and password. The system will save the user in a repository and simulate sending a notification to the user after registration. The mail server settings (such a host and port) for sending notifications should be configurable via the application.properties file. This is a simulation, and no actual emails will be sent.

# Documentation – User Registration Service (Spring Boot)

## 1. Project Title

User Registration Service using Spring Boot

---

# 2. Objective

The objective of this project is to implement a **User Registration Service** using Spring Boot. The application allows a user to register by providing their **name**, **email**, and **password**. The user information is stored in an **in-memory repository**, and after successful registration, the application simulates sending an email notification.

The mail server configuration (host and port) is externalized in the **application.yml** file using Spring's `@Value` annotation.

---

# 3. Features

- Register a new user
- Prevent duplicate registrations using email
- Store users in an in-memory repository
- Simulate email notification
- Externalize mail server configuration
- Demonstrate Dependency Injection
- Demonstrate Constructor Injection
- Demonstrate Repository and Service layers

---

# 4. Technologies Used

- Java
- Spring Boot
- Spring Core (IoC & Dependency Injection)
- Maven
- YAML Configuration (`application.yml`)

---

# 5. Project Structure

```
registrationservice
│
├── RegistrationServiceApplication.java
├── User.java
│
├── UserRepository.java
├── InMemoryUserRepository.java
│
├── NotificationService.java
├── EmailNotificationService.java
│
├── UserService.java
│
└── application.yml
```

---

# 6. Class Diagram

```
                +----------------------+
                | NotificationService  |
                +----------------------+
                | +send()              |
                +----------^-----------+
                           |
             implements
                           |
         +------------------------------+
         | EmailNotificationService     |
         +------------------------------+

                +-------------------+
                | UserRepository    |
                +-------------------+
                | +save()           |
                | +findByEmail()    |
                +---------^---------+
                          |
                implements
                          |
        +------------------------------+
        | InMemoryUserRepository       |
        +------------------------------+

                    +----------------+
                    |     User       |
                    +----------------+

                    +----------------+
                    | UserService    |
                    +----------------+
                    | registerUser() |
                    +----------------+
                     |           |
                     |           |
         UserRepository   NotificationService
```

---

# 7. Component Description

## 7.1 User

Represents a registered user.

### Fields

| Field    | Type   | Description   |
| -------- | ------ | ------------- |
| id       | long   | User ID       |
| email    | String | User email    |
| password | String | User password |
| name     | String | User name     |

---

## 7.2 UserRepository

Interface responsible for user storage.

```java
void save(User user);

User findByEmail(String email);
```

Responsibilities

- Save user
- Search user by email

---

## 7.3 InMemoryUserRepository

Implementation of `UserRepository`.

Annotation:

```java
@Repository
```

Stores users inside a

```java
Map<String, User>
```

where

```
Key   → Email
Value → User Object
```

Methods:

### save()

Stores user in HashMap.

```java
users.put(user.getEmail(), user);
```

### findByEmail()

Returns the user if found.

```java
users.getOrDefault(email, null);
```

---

## 7.4 NotificationService

Notification abstraction.

```java
void send(String message,
          String recipientEmail);
```

---

## 7.5 EmailNotificationService

Implementation of NotificationService.

Annotation:

```java
@Service("email")
@Primary
```

Uses configuration values from

```
application.yml
```

through

```java
@Value("${mail.host}")
private String host;

@Value("${mail.port}")
private String port;
```

Instead of sending an actual email, it prints:

```
Recipient
Message
Mail Host
Mail Port
```

---

## 7.6 UserService

Business logic layer.

Annotation

```java
@Service
```

Dependencies

```java
private final UserRepository userRepository;

private final NotificationService notificationService;
```

Injected through constructor.

Main Method

```java
registerUser(User user)
```

Workflow

```
Receive User
↓
Check if email already exists
↓
If yes
Throw Exception
↓
If no
↓
Save User
↓
Send Notification
```

---

## 7.7 RegistrationServiceApplication

Main Spring Boot application.

```java
@SpringBootApplication
```

Starts Spring Boot and retrieves the `UserService` bean from the application context.

Example:

```java
var userService = context.getBean(UserService.class);

userService.registerUser(
    new User(
        1L,
        "s@gmail.com",
        "12345",
        "Siyam Hossain"
    )
);
```

---

# 8. Dependency Injection

Spring automatically injects dependencies through constructor injection.

```java
public UserService(
        UserRepository userRepository,
        NotificationService notificationService
)
```

Spring provides:

- InMemoryUserRepository
- EmailNotificationService

without creating them manually using `new`.

---

# 9. External Configuration

Configuration stored in

```
application.yml
```

```yaml
mail:
    host: https://smtp.gmail.com
    port: 8080
```

Read using

```java
@Value("${mail.host}")
```

and

```java
@Value("${mail.port}")
```

Advantages

- No hard-coded values
- Easy to change configuration
- Environment specific configuration

---

# 10. Registration Process

```
User
↓
UserService.registerUser()
↓
findByEmail()
↓
Already Exists?
        │
   Yes ─┴──► Exception
No
↓
save(user)
↓
send notification
↓
Registration Successful
```

---

# 11. Program Execution

### First Registration

```
saving user:
User{id=1, email=s@gmail.com, ...}

recipient: s@gmail.com

message:
You registered successfully

Host:
https://smtp.gmail.com

Port:
8080
```

### Second Registration

Since the same email already exists,

```
IllegalArgumentException:

user with email:
s@gmail.com already exists
```

---

# 12. Spring Annotations Used

| Annotation               | Purpose                                                      |
| ------------------------ | ------------------------------------------------------------ |
| `@SpringBootApplication` | Starts Spring Boot application                               |
| `@Service`               | Marks service classes                                        |
| `@Repository`            | Marks repository class                                       |
| `@Primary`               | Chooses the default bean when multiple implementations exist |
| `@Value`                 | Injects configuration values from `application.yml`          |

---

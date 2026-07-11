# Bean Scopes

- Singleton
- Prototype
- Request
- Session

---

# Project Structure

```text
src
 └── main
      ├── java
      │      └── com.sh.beanscopes
      │             │
      │             ├── BeanScopesApplication.java
      │             ├── AppConfig.java
      │             ├── PaymentService.java
      │             ├── StripePaymentService.java
      │             ├── PayPalPaymentService.java
      │             └── OrderService.java
      │
      └── resources
             └── application.yaml
```

---

# 1. PaymentService.java

```java
package com.sh.beanscopes;

public interface PaymentService {

    void processPayment(double amount);

}
```

---

# 2. StripePaymentService.java

```java
package com.sh.beanscopes;

public class StripePaymentService implements PaymentService {

    public StripePaymentService() {
        System.out.println("StripePaymentService Created");
    }

    @Override
    public void processPayment(double amount) {

        System.out.println("Stripe Payment");
        System.out.println("Amount : " + amount);

    }

}
```

---

# 3. PayPalPaymentService.java

```java
package com.sh.beanscopes;

public class PayPalPaymentService implements PaymentService {

    public PayPalPaymentService() {
        System.out.println("PayPalPaymentService Created");
    }

    @Override
    public void processPayment(double amount) {

        System.out.println("PayPal Payment");
        System.out.println("Amount : " + amount);

    }

}
```

---

# 4. OrderService.java

```java
package com.sh.beanscopes;

public class OrderService {

    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {

        System.out.println("OrderService Created");

        this.paymentService = paymentService;

    }

    public void placeOrder() {

        paymentService.processPayment(100);

    }

}
```

---

# 5. AppConfig.java

```java
package com.sh.beanscopes;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Scope;

@Configuration
public class AppConfig {

    @Value("${payment-gateway}")
    private String paymentGateway;

    @Bean
    public PaymentService stripe() {

        return new StripePaymentService();

    }

    @Bean
    public PaymentService paypal() {

        return new PayPalPaymentService();

    }

    @Bean
    @Scope("prototype")
    public OrderService orderService() {

        if (paymentGateway.equalsIgnoreCase("stripe")) {
            return new OrderService(stripe());
        }

        return new OrderService(paypal());

    }

}
```

---

# 6. BeanScopesApplication.java

```java
package com.sh.beanscopes;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class BeanScopesApplication {

    public static void main(String[] args) {

        ApplicationContext context =
                SpringApplication.run(BeanScopesApplication.class, args);

        OrderService order1 = context.getBean(OrderService.class);
        OrderService order2 = context.getBean(OrderService.class);

        System.out.println(order1);
        System.out.println(order2);

    }

}
```

---

# 7. application.yaml

```yaml
spring:
    application:
        name: BeanScopes

payment-gateway: stripe
```

---

# Output (Prototype Scope)

```text
StripePaymentService Created

OrderService Created

OrderService Created

com.sh.beanscopes.OrderService@5a07e868

com.sh.beanscopes.OrderService@76ed5528
```

Notice

```text
OrderService Created
```

appears **twice**.

Also,

```text
@5a07e868
```

and

```text
@76ed5528
```

are different memory addresses.

---

# What is Bean Scope?

A **bean scope** defines **how many objects Spring creates** and **how long those objects live**.

When you ask Spring for a bean:

```java
context.getBean(OrderService.class);
```

Should Spring:

- return the same object every time?
- create a new object every time?
- create one object per HTTP request?
- create one object per user session?

The answer depends on the bean's **scope**.

---

# The Four Main Bean Scopes

| Scope     | Number of Objects                          |
| --------- | ------------------------------------------ |
| Singleton | One object for the entire Spring container |
| Prototype | A new object every time it is requested    |
| Request   | One object per HTTP request                |
| Session   | One object per HTTP session                |

---

# 1. Singleton Scope (Default)

If you don't specify a scope:

```java
@Bean
public OrderService orderService() {

    return new OrderService(stripe());

}
```

Spring automatically uses:

```java
@Scope("singleton")
```

even though you don't write it.

---

Suppose you do

```java
OrderService a = context.getBean(OrderService.class);

OrderService b = context.getBean(OrderService.class);
```

Spring behaves like this

```
Spring Container

OrderService
      │
      ▼
 ONE OBJECT
```

Both variables point to the same object.

```
a ───────┐
         │
         ▼
     OrderService
         ▲
         │
b ───────┘
```

Output

```
OrderService Created

com.example.OrderService@12345

com.example.OrderService@12345
```

Notice

Both addresses are identical.

Only one object exists.

---

# Why Singleton?

Most services are stateless.

Example

```
UserService

OrderService

EmailService

PaymentService
```

These services don't store user-specific data.

Creating multiple copies wastes memory.

Singleton saves resources.

---

# 2. Prototype Scope

Your code

```java
@Bean
@Scope("prototype")
public OrderService orderService() {

    return new OrderService(stripe());

}
```

Now Spring behaves differently.

Every call

```java
context.getBean(OrderService.class);
```

creates a brand new object.

```
getBean()
↓
Create Object
↓
Return Object
```

Second call

```
getBean()
↓
Create Another Object
↓
Return Object
```

Diagram

```
order1
↓
OrderService A


order2
↓
OrderService B
```

Two completely different objects.

---

Output

```
OrderService Created

OrderService Created

@12345

@56789
```

---

Why use Prototype?

Suppose you're building a drawing application.

Every shape is different.

```
Circle

Rectangle

Triangle
```

Each needs its own object.

Sharing one object would be incorrect.

Prototype is appropriate when each caller needs an independent instance.

---

# 3. Request Scope

Used only in **Spring Web (Spring MVC/REST)**.

```java
@RequestScope
@Component
public class ShoppingCart {

}
```

Imagine two users send requests.

```
Request 1
↓
ShoppingCart A
```

```
Request 2
↓
ShoppingCart B
```

Each HTTP request gets its own bean.
When the request ends, the bean is destroyed.

Typical uses:

- Request metadata
- Authentication details
- Temporary calculations

---

# 4. Session Scope

Also used in web applications.

```java
@SessionScope
@Component
public class UserPreferences {

}
```

Suppose

Alice logs in.

```
Session
↓
UserPreferences
```

Alice makes 20 requests.

The same bean is reused.

Bob logs in.

```
New Session
↓
Another UserPreferences
```

Each user session gets its own bean.

Useful for:

- Shopping carts
- User preferences
- Login information

---

# Scope Comparison

```
Singleton

Application
    │
    ▼
 ONE OBJECT
```

---

```
Prototype

getBean()
↓
New Object
↓
getBean()
↓
Another New Object
```

---

```
Request

HTTP Request 1
↓
Object A

HTTP Request 2
↓
Object B
```

---

```
Session

User A
↓
Object A

User B
↓
Object B
```

---

# Which Scope Should You Use?

| Scope     | Typical Use Case                                                     |
| --------- | -------------------------------------------------------------------- |
| Singleton | Services, repositories, controllers, configuration classes           |
| Prototype | Independent objects that should not be shared                        |
| Request   | Data that exists only during a single HTTP request                   |
| Session   | Data that should persist across multiple requests from the same user |

---

# Important Interview Point

> **Singleton is the default scope in Spring.**

If you don't write:

```java
@Scope("singleton")
```

Spring still creates a singleton bean.

That's why most Spring applications don't explicitly specify the singleton scope—it is the default behavior.

In contrast, you only need to add `@Scope("prototype")`, `@RequestScope`, or `@SessionScope` when you want behavior different from the default.

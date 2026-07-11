# Project Structure

```text
src
 └── main
      ├── java
      │      └── com.sh.beanlifecyclehooks
      │             │
      │             ├── BeanLifecycleHooksApplication.java
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
package com.sh.beanlifecyclehooks;

public interface PaymentService {

    void processPayment(double amount);

}
```

---

# 2. StripePaymentService.java

```java
package com.sh.beanlifecyclehooks;

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
package com.sh.beanlifecyclehooks;

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
package com.sh.beanlifecyclehooks;

import jakarta.annotation.PostConstruct;
import jakarta.annotation.PreDestroy;

public class OrderService {

    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {

        System.out.println("---------------------------");
        System.out.println("OrderService Constructor");
        System.out.println("---------------------------");

        this.paymentService = paymentService;

    }

    @PostConstruct
    public void init() {

        System.out.println("---------------------------");
        System.out.println("PostConstruct Executed");
        System.out.println("---------------------------");

    }

    @PreDestroy
    public void cleanup() {

        System.out.println("---------------------------");
        System.out.println("PreDestroy Executed");
        System.out.println("---------------------------");

    }

    public void placeOrder() {

        paymentService.processPayment(100);

    }

}
```

---

# 5. AppConfig.java

```java
package com.sh.beanlifecyclehooks;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

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
    public OrderService orderService() {

        if (paymentGateway.equalsIgnoreCase("stripe")) {
            return new OrderService(stripe());
        }

        return new OrderService(paypal());

    }

}
```

---

# 6. BeanLifecycleHooksApplication.java

```java
package com.sh.beanlifecyclehooks;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class BeanLifecycleHooksApplication {

    public static void main(String[] args) {

        ConfigurableApplicationContext context =
                SpringApplication.run(
                        BeanLifecycleHooksApplication.class,
                        args
                );

        OrderService orderService = context.getBean(OrderService.class);

        orderService.placeOrder();

        context.close();

    }

}
```

---

# 7. application.yaml

```yaml
spring:
    application:
        name: BeanLifecycleHooks

payment-gateway: stripe
```

---

# Output

```text
StripePaymentService Created

---------------------------
OrderService Constructor
---------------------------

---------------------------
PostConstruct Executed
---------------------------

Stripe Payment
Amount : 100.0

---------------------------
PreDestroy Executed
---------------------------
```

---

# What is Bean Lifecycle?

Every Spring bean has a lifecycle.

It is **born**, **used**, and eventually **destroyed**.

Just like a person:

```text
Birth
↓
Childhood
↓
Adult Life
↓
Death
```

A Spring bean goes through similar stages.

```text
Create Bean
↓
Initialize Bean
↓
Use Bean
↓
Destroy Bean
```

Spring lets us execute custom code at specific points in this lifecycle.
These are called **Lifecycle Hooks**.

---

# Bean Lifecycle Steps

A singleton bean typically follows these stages:

```text
Application Starts
↓
Spring Creates Bean
↓
Dependency Injection
↓
@PostConstruct
↓
Bean Ready
↓
Application Running
↓
@PreDestroy
↓
Bean Destroyed
```

---

# Step 1: Constructor

```java
public OrderService(PaymentService paymentService) {

    System.out.println("OrderService Constructor");

    this.paymentService = paymentService;

}
```

This runs when Spring creates the object.

At this point:

- the object exists,
- constructor injection has occurred,
- but initialization callbacks haven't run yet.

Output:

```text
OrderService Constructor
```

---

# Step 2: Dependency Injection

Spring injects the required dependencies.

```text
OrderService
↓
PaymentService
```

After all dependencies are available, Spring proceeds to initialization.

---

# Step 3: `@PostConstruct`

```java
@PostConstruct
public void init() {

    System.out.println("PostConstruct Executed");

}
```

This method is called **exactly once**, immediately after:

- object creation,
- dependency injection,
- bean configuration.
  It runs before any other bean starts using this bean.

---

### Why use `@PostConstruct`?

Initialize resources such as:

- loading configuration
- opening files
- initializing caches
- validating configuration
- creating expensive objects

Example:

```java
@PostConstruct
public void loadCache() {

    cache.loadAllProducts();

}
```

Without `@PostConstruct`, you'd have to remember to call `loadCache()` manually. Spring does it automatically.

---

# Step 4: Bean Ready

Now the bean is fully initialized.
You can safely use it.

```java
OrderService order = context.getBean(OrderService.class);

order.placeOrder();
```

---

# Step 5: `@PreDestroy`

```java
@PreDestroy
public void cleanup() {

    System.out.println("PreDestroy Executed");

}
```

This method is called **before Spring destroys the bean**.

---

### Why use `@PreDestroy`?

Release resources such as:

- database connections
- sockets
- files
- thread pools
- caches

Example:

```java
@PreDestroy
public void closeConnection() {

    connection.close();

}
```

Without it, resources may remain open and cause leaks.

---

# Why do we call `context.close()`?

Your application uses:

```java
ConfigurableApplicationContext context =
        SpringApplication.run(...);
```

Then:

```java
context.close();
```

Closing the context tells Spring:

> "The application is shutting down. Destroy all singleton beans."

During shutdown Spring:

```text
Close Context
↓
Call @PreDestroy
↓
Destroy Bean
```

If you don't close the context manually, Spring Boot normally closes it automatically when the application exits.

---

# Complete Lifecycle Timeline

```text
Spring Starts
        │
        ▼
Create Object
(Constructor)
        │
        ▼
Inject Dependencies
        │
        ▼
@PostConstruct
        │
        ▼
Bean Ready
        │
        ▼
Application Running
        │
        ▼
@PreDestroy
        │
        ▼
Bean Destroyed
```

---

# When are these hooks called?

| Hook             | When it executes                                    |
| ---------------- | --------------------------------------------------- |
| Constructor      | Immediately when Spring creates the bean            |
| `@PostConstruct` | After dependency injection, before the bean is used |
| Business Methods | Whenever your application calls them                |
| `@PreDestroy`    | Just before the bean is destroyed                   |

---

# Important Notes

### 1. `@PostConstruct` runs only once

Even if you call:

```java
context.getBean(OrderService.class);
context.getBean(OrderService.class);
```

`@PostConstruct` is executed only once for a singleton bean because only one instance exists.

---

### 2. `@PreDestroy` works for singleton beans

For singleton beans, Spring manages both creation and destruction, so it can invoke `@PreDestroy`.

For **prototype** beans, Spring creates the bean but does **not** manage its full lifecycle after returning it. As a result, `@PreDestroy` is **not called automatically** for prototype-scoped beans.

---

# Real-World Examples

| Hook             | Common Uses                                                        |
| ---------------- | ------------------------------------------------------------------ |
| Constructor      | Basic object creation                                              |
| `@PostConstruct` | Load cache, validate configuration, initialize resources           |
| Business Methods | Process orders, handle requests, perform application logic         |
| `@PreDestroy`    | Close database connections, stop threads, release files or sockets |

---

# Constructor vs `@PostConstruct`

| Constructor                                             | `@PostConstruct`                                       |
| ------------------------------------------------------- | ------------------------------------------------------ |
| Creates the object                                      | Initializes the fully constructed object               |
| Runs during object creation                             | Runs after dependency injection is complete            |
| Dependencies may still be in the process of being wired | All injected dependencies are available and ready      |
| Used for basic construction                             | Used for initialization that depends on injected beans |

A good rule of thumb is:

- Use the **constructor** to establish the object's required state.
- Use **`@PostConstruct`** for initialization that depends on injected dependencies or requires the bean to be fully configured.
- Use **`@PreDestroy`** to clean up resources before the bean is removed from the Spring container.

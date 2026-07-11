# Project Structure

```text
src
 └── main
      ├── java
      │      └── com.sh.lazyinitialization
      │             │
      │             ├── LazyInitializationApplication.java
      │             ├── HeavyResource.java
      │             ├── PaymentService.java
      │             ├── StripePaymentService.java
      │             ├── OrderService.java
      │             └── AppConfig.java
      │
      └── resources
             └── application.yaml
```

---

# 1. PaymentService.java

```java
package com.sh.lazyinitialization;

public interface PaymentService {

    void processPayment(double amount);

}
```

---

# 2. StripePaymentService.java

```java
package com.sh.lazyinitialization;

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

# 3. OrderService.java

```java
package com.sh.lazyinitialization;

public class OrderService {

    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
        System.out.println("OrderService Created");
    }

    public void placeOrder() {

        paymentService.processPayment(100);

    }

}
```

---

# 4. HeavyResource.java

```java
package com.sh.lazyinitialization;

import org.springframework.context.annotation.Lazy;
import org.springframework.stereotype.Component;

@Component
@Lazy
public class HeavyResource {

    public HeavyResource() {

        System.out.println("Heavy Resource Created");

    }

}
```

---

# 5. AppConfig.java

```java
package com.sh.lazyinitialization;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class AppConfig {

    @Bean
    public PaymentService paymentService() {

        return new StripePaymentService();

    }

    @Bean
    public OrderService orderService(PaymentService paymentService) {

        return new OrderService(paymentService);

    }

}
```

---

# 6. LazyInitializationApplication.java

```java
package com.sh.lazyinitialization;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class LazyInitializationApplication {

    public static void main(String[] args) {

        ApplicationContext context =
                SpringApplication.run(LazyInitializationApplication.class, args);

        System.out.println("Application Started");

        HeavyResource resource = context.getBean(HeavyResource.class);

    }

}
```

---

# application.yaml

```yaml
spring:
    application:
        name: LazyInitialization
```

---

# Output

```text
StripePaymentService Created
OrderService Created
Application Started
Heavy Resource Created
```

Notice something interesting:

The application starts **before** `HeavyResource` is created.

---

# What is Lazy Initialization?

Normally, Spring creates all singleton beans when the application starts.

This is called **Eager Initialization**.

```
Application Starts
        │
        ▼
Create Bean A
Create Bean B
Create Bean C
Create Bean D
```

Everything is ready before your application begins serving requests.

---

## Without `@Lazy`

```java
@Component
public class HeavyResource {

}
```

Output

```text
Heavy Resource Created
Application Started
```

Spring creates it immediately during startup.

---

## With `@Lazy`

```java
@Component
@Lazy
public class HeavyResource {

}
```

Output

```text
Application Started

Heavy Resource Created
```

The bean is created only when it is actually requested.

---

# How does it work internally?

Suppose you have

```java
@Component
@Lazy
public class HeavyResource {

}
```

Spring does **not** create the object immediately.

Instead, it stores the bean definition.

```
Spring Container

HeavyResource
      │
      ▼
Bean Definition
```

No object exists yet.

---

Later,

```java
context.getBean(HeavyResource.class);
```

Spring checks

```
Is object already created?

No
```

↓
Creates it
↓
Stores it
↓
Returns it

```
Spring Container

HeavyResource
      │
      ▼
HeavyResource Object
```

---

If you call again

```java
context.getBean(HeavyResource.class);
```

- Spring simply returns the existing singleton.
- No new object is created.

---

# Why is it useful?

Imagine a bean that

- connects to a database
- loads a 500 MB machine learning model
- initializes a payment gateway
- loads thousands of files

Initialization may take several seconds.
If users never use that feature, creating it during startup wastes time and memory.
Lazy initialization avoids that.

---

Example

```
PDF Generator

Image Processor

Machine Learning Model

Email Sender
```

Suppose only **5%** of users generate PDFs.

Without Lazy

```
Application Starts
↓
Create PDF Generator
↓
Create Image Processor
↓
Create ML Model
↓
Create Email Sender
```

Everything is initialized.

---

With Lazy

```
Application Starts
↓
Nothing expensive created
↓
User clicks "Generate PDF"
↓
Create PDF Generator
```

Only needed resources are created.

---

# Benefits

## Faster startup

Instead of

```
10 seconds
```

startup may become

```
3 seconds
```

because expensive beans are delayed.

---

## Lower memory usage

Unused objects aren't created.

Example

```
Report Generator

Excel Generator

PDF Generator
```

If users only generate PDFs,

Excel Generator is never instantiated.

---

## Better for expensive resources

Examples include:

- AI models
- Database pools
- Payment SDKs
- File parsers
- Cache builders

---

# Drawbacks

Suppose the first user requests

```
Generate Report
```

Spring now creates

```
HeavyResource
```

The first request may wait 2–3 seconds.

Later requests are fast because the singleton already exists.

---

# Eager vs Lazy

## Eager

```
Application Starts
↓
Create Everything
↓
Ready
```

Advantages

- First request is fast.
- Startup validates that all beans can be created.

Disadvantages

- Slower startup.
- Higher memory usage.

---

## Lazy

```
Application Starts
↓
Create Nothing
↓
User Needs Bean
↓
Create Bean
```

Advantages

- Faster startup.
- Saves memory.
- Doesn't initialize unused beans.

Disadvantages

- First use is slower.
- Configuration errors in a lazy bean may not be discovered until that bean is accessed.

---

# Global Lazy Initialization

Instead of marking individual beans,

```java
@Lazy
@Component
public class HeavyResource {

}
```

Spring Boot also supports enabling lazy initialization for **all** beans:

```yaml
spring:
    main:
        lazy-initialization: true
```

Now every bean is lazy unless you explicitly override it.

This should be used carefully, because it delays bean creation and error detection throughout the application.

---

# "Premature optimization is the root of all evil"

This famous quote from Donald Knuth means:

> **Don't optimize something before you know it's actually a problem.**

- Suppose your application starts in **1.5 seconds**.
- You spend two days making every bean lazy to reduce startup to **1.2 seconds**.
- Users don't notice the difference.
- You made the code more complex without solving a real problem.
- That's **premature optimization**.

A better approach is:

1. Build a correct application.
2. Measure its performance.
3. Identify actual bottlenecks.
4. Optimize only where it provides meaningful benefit.

Lazy initialization is a valuable optimization when startup time or resource usage is genuinely an issue—for example, in large applications or when some beans are expensive to construct. In small applications, adding `@Lazy` everywhere usually provides little benefit and can make debugging harder by postponing errors until runtime.

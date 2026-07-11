# Correct Project

```
src
 └── main
      ├── java
      │      └── com.sh.beansusingcode
      │             │
      │             ├── BeansUsingCodeApplication.java
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

# PaymentService.java

```java
package com.sh.beansusingcode;

public interface PaymentService {

    void processPayment(double amount);

}
```

---

# StripePaymentService.java

```java
package com.sh.beansusingcode;

import org.springframework.beans.factory.annotation.Value;

import java.util.List;

public class StripePaymentService implements PaymentService {

    @Value("${stripe.apiUrl}")
    private String apiUrl;

    @Value("${stripe.enabled}")
    private boolean enabled;

    @Value("${stripe.supported-currencies}")
    private List<String> currency;

    @Value("${stripe.timeout}")
    private int timeout;

    @Override
    public void processPayment(double amount) {

        System.out.println("STRIPE");
        System.out.println("Amount : " + amount);

        System.out.println("API URL : " + apiUrl);
        System.out.println("Enabled : " + enabled);
        System.out.println("Currencies : " + currency);
        System.out.println("Timeout : " + timeout);

    }
}
```

---

# PayPalPaymentService.java

```java
package com.sh.beansusingcode;

public class PayPalPaymentService implements PaymentService {

    @Override
    public void processPayment(double amount) {

        System.out.println("PAYPAL");
        System.out.println("Amount : " + amount);

    }

}
```

---

# OrderService.java

```java
package com.sh.beansusingcode;

public class OrderService {

    private final PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }

    public void placeOrder() {

        paymentService.processPayment(100);

    }

}
```

---

# AppConfig.java

```java
package com.sh.beansusingcode;

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

# BeansUsingCodeApplication.java

```java
package com.sh.beansusingcode;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class BeansUsingCodeApplication {

    public static void main(String[] args) {

        ApplicationContext context = SpringApplication.run(BeansUsingCodeApplication.class, args);

        OrderService orderService = context.getBean(OrderService.class);

        orderService.placeOrder();

    }

}
```

---

# application.yaml

```yaml
spring:
    application:
        name: BeansUsingCode

stripe:
    apiUrl: https://api.stripe.com
    enabled: true
    timeout: 1000
    supported-currencies:
        - USD
        - EUR
        - GBP

payment-gateway: stripe
```

or

```yaml
payment-gateway: paypal
```

---

# Output (Stripe)

```
STRIPE
Amount : 100.0
API URL : https://api.stripe.com
Enabled : true
Currencies : [USD, EUR, GBP]
Timeout : 1000
```

---

# Output (PayPal)

```
PAYPAL
Amount : 100.0
```

---

# Concept: Configuring Beans Using Code

Previously, you used annotations like:

```java
@Service
public class StripePaymentService {
}
```

Spring automatically discovered the class during component scanning and created the bean.

This is called **annotation-based configuration**.

---

## Configuring Beans Using Java Code

Instead of letting Spring discover beans automatically, you can create them yourself in a configuration class.

```java
@Configuration
public class AppConfig {
}
```

`@Configuration` tells Spring:

> "This class contains bean definitions."

---

## What is `@Bean`?

```java
@Bean
public PaymentService stripe() {

    return new StripePaymentService();

}
```

When Spring starts:

1. It creates an `AppConfig` object.
2. It calls the `stripe()` method.
3. It stores the returned object in the IoC container.

So this:

```java
@Bean
public PaymentService stripe() {
    return new StripePaymentService();
}
```

is roughly equivalent to:

```java
@Service
public class StripePaymentService {
}
```

The difference is that **you decide exactly how the object is created**.

---

## How does `OrderService` get its dependency?

Your configuration contains:

```java
@Bean
public OrderService orderService() {

    return new OrderService(stripe());

}
```

Spring first creates:

```
StripePaymentService
```

Then passes it into:

```
OrderService
```

The object graph looks like:

```
Spring Container
        │
        ├───────────────┐
        │               │
 StripePaymentService   OrderService
                            │
                            ▼
                   PaymentService
```

---

## Dynamic Bean Selection

A powerful feature of Java configuration is that you can decide which implementation to inject at runtime.

```java
@Bean
public OrderService orderService() {

    if (paymentGateway.equalsIgnoreCase("stripe")) {
        return new OrderService(stripe());
    }

    return new OrderService(paypal());

}
```

If the configuration contains:

```yaml
payment-gateway: stripe
```

then `OrderService` receives a `StripePaymentService`.

If it contains:

```yaml
payment-gateway: paypal
```

then `OrderService` receives a `PayPalPaymentService`.

No Java code changes are required—only the configuration changes.

---

## Why use Java Configuration?

Using `@Configuration` and `@Bean` is useful when:

- You need to choose implementations based on configuration.
- You want full control over how objects are created.
- You need to configure third-party classes that you cannot annotate with `@Service`.
- You want conditional or programmatic bean creation.

For simple applications, `@Service`, `@Component`, and `@Repository` are usually enough. For more advanced scenarios requiring explicit control, Java-based configuration with `@Configuration` and `@Bean` is the preferred approach.

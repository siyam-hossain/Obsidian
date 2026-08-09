### Configure Bin

1.  Using Annotation
2.  Using Code

Type of annotations

| **Annotations** | **Work type**            | **What it can do**                                                                                                                                                                         |
| --------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `@Component`    | Generic Spring bean      | Marks a class as a generic Spring-managed bean so it can be detected during component scanning and managed by the Spring IoC container.                                                    |
| `@Service`      | Business logic           | Marks a class as part of the service/business logic layer. It is a specialized form of `@Component` used for service classes.                                                              |
| `@Repository`   | Database access          | Marks a class as part of the data access (DAO) layer. It is a specialized `@Component` and also enables automatic translation of database exceptions into Spring's data access exceptions. |
| `@Controller`   | Handles we request (MVC) | Marks a class as a Spring MVC controller that handles HTTP requests and returns views or delegates responses. It is a specialized form of `@Component`.                                    |
| `@Autowired`    | dependency injection.    | Find a suitable bean from the Spring container and inject it here.                                                                                                                         |

Note:

- `@Service` is a alias of `@Component`

---

### Now let's fix the previous section bug

> [!bug]
> Exception in thread "main" org.springframework.beans.factory.NoSuchBeanDefinitionException: No qualifying bean of type 'com.sh.thespringioccontainer.OrderService' available
>
> > ```
> > at org.springframework.beans.factory.support.DefaultListableBeanFactory.getBean(DefaultListableBeanFactory.java:386)
> > at org.springframework.beans.factory.support.DefaultListableBeanFactory.getBean(DefaultListableBeanFactory.java:377>)
> > at org.springframework.context.support.AbstractApplicationContext.getBean(AbstractApplicationContext.java:1317)
> > at com.sh.thespringioccontainer.TheSpringIoCContainerApplication.main(TheSpringIoCContainerApplication.java:12)
> > ```

#### Classes

_ConfigureBinsUsingAnnotationsApplication_

```java
package com.sh.configurebinsusingannotations;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class ConfigureBinsUsingAnnotationsApplication {

    public static void main(String[] args) {
        ApplicationContext context = SpringApplication.run(ConfigureBinsUsingAnnotationsApplication.class, args);
        var orderService = context.getBean(OrderService.class);
        orderService.placeOrder();
    }
}
```

_PaymentService_

```java
package com.sh.configurebinsusingannotations;

public interface PaymentService {
    void processPayment(double amount);
}
```

_PaypalPaymentService_

```java
package com.sh.configurebinsusingannotations;

import org.springframework.stereotype.Service;

@Service
public class PaypalPaymentService implements PaymentService {
    @Override
    public void processPayment(double amount) {
        System.out.println("PayPal");
        System.out.println("Amount: "+amount);
    }
}
```

---

Here,

- I use `@service` annotation
- `@Service` tells Spring that `PaypalPaymentService` is a **service bean** that should be automatically created and managed by the Spring container.

**_What happens because of `@Service`?_**
When Spring starts:

1. Component scanning finds the class because it is annotated with `@Service`.
2. Spring creates one instance (a bean) of `PaypalPaymentService` by default.
3. The bean is stored in the Spring IoC container.
4. Whenever another class needs a `PaymentService`, Spring can automatically inject this bean.

---

_OrderService_

```java
package com.sh.configurebinsusingannotations;

import org.springframework.stereotype.Component;
import org.springframework.stereotype.Service;

@Service
public class OrderService {
    private PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }

    public void setPaymentService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }

    public void placeOrder(){
        paymentService.processPayment(10);
    }
}
```

Why is `OrderService` also annotated?

Because Spring must manage both objects.

```
Spring Container
-----------------------------
OrderService            <-- @Service
PaypalPaymentService    <-- @Service
```

When creating `OrderService`, Spring says:

- "Its constructor needs a `PaymentService`. Do I already have one?"
  Yes:

```
PaypalPaymentService implements PaymentService
```

So Spring injects it.

Think of it like this,

Imagine a company:

- `OrderService` = Order manager
- `PaypalPaymentService` = Cashier
- The order manager can't work unless there is a cashier.

---

> [!Output:]
>
> > PayPal
> > Amount: 10.0

---

### @Autowired

_Example 1: Constructor Injection (Recommended_

```java
@Service
public class OrderService {

    private PaymentService paymentService;

    @Autowired
    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

Spring does this automatically:

```java
PaymentService paymentService = new PaypalPaymentService();
OrderService orderService = new OrderService(paymentService);
```

You don't have to create the objects ourselves.

---

_Example 2: Field Injection_

```java
@Service
public class OrderService {

    @Autowired
    private PaymentService paymentService;
}
```

Spring injects the `PaymentService` directly into the field.

---

_Example 3: Setter Injection_

```
@Service
public class OrderService {

    private PaymentService paymentService;

    @Autowired
    public void setPaymentService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}
```

Spring calls the setter after creating the object.

---

### How does `@Autowired` work?

Suppose we have:

```java
@Service
public class PaypalPaymentService implements PaymentService {
}
```

and

```java
@Service
public class OrderService {

    @Autowired
    private PaymentService paymentService;
}
```

When Spring starts:

1. It scans for beans.
2. It creates a `PaypalPaymentService` bean.
3. It creates an `OrderService` bean.
4. It notices the `@Autowired` field.
5. It searches for a bean of type `PaymentService`.
6. It finds `PaypalPaymentService`.
7. It injects it

---

### When is `@Autowired` required?

| Injection Type                      | Is `@Autowired` Required?                                |
| ----------------------------------- | -------------------------------------------------------- |
| Constructor (only one constructor)  | ❌ No                                                    |
| Constructor (multiple constructors) | ✅ Yes (to indicate which constructor Spring should use) |
| Field injection                     | ✅ Yes                                                   |
| Setter injection                    | ✅ Yes                                                   |

Note: ==Remember when multiple constructor present for a single class we should apply `@Autowired` only one constructor==

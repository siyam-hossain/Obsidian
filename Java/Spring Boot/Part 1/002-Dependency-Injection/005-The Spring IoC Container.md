**What is the IoC Container?**
The IoC (Inversion of Control) Container is the core part of Spring that:

- Creates objects (called beans)
- Stores them
- Injects dependencies between them
- Manages their lifecycle

**Instead of you writing:**

```java
PaymentService paymentService = new PaypalPaymentService();
OrderService orderService = new OrderService(paymentService);
```

the IoC container does this work for you.

---

## **Classes**

_PaymentService_

```java
public interface PaymentService {
    void processPayment(double amount);
}
```

This is just a contract

_PaypalPaymentService_

```java
public class PaypalPaymentService implements PaymentService {

    @Override
    public void processPayment(double amount) {
        System.out.println("PayPal");
        System.out.println("Amount: " + amount);
    }
}
```

This is the implementation of `PaymentService`.

_OrderService_

```java
public class OrderService {

    private PaymentService paymentService;

    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }

    public void placeOrder() {
        paymentService.processPayment(10);
    }
}
```

Notice something important.
`OrderService` does not create a `PaypalPaymentService`.

It only says:

- "Someone give me any object that implements `PaymentService`."
- That "someone" is the IoC Container.

---

_What happens when the application starts?_

```java
ApplicationContext context = SpringApplication.run(TheSpringIoCContainerApplication.class, args);
```

This line starts Spring.

When Spring starts, it creates the IoC Container.

```text
Application Starts
        │
        ▼
SpringApplication.run()
        │
        ▼
IoC Container Created
```

---

# Next Step

The container scans our project.

```
Project
│
├── OrderService
├── PaypalPaymentService
└── PaymentService
```

It looks for Spring-managed classes like

```
@Component
@Service
@Repository
@Controller
@Configuration
```

(Our example doesn't have these yet, but we're ignoring that for now.)

---

# Bean Creation

The IoC container creates objects.

```
IoC Container

--------------------------
OrderService Object
--------------------------

--------------------------
PaypalPaymentService Object
--------------------------
```

- These objects are called Beans.
- A Bean is simply an object managed by Spring.

---

# Dependency Injection

Now Spring sees

```java
public OrderService(PaymentService paymentService)
```

It asks:

- "Who implements PaymentService?"

It finds

```
PaypalPaymentService
```

So Spring performs constructor injection.

Internally it does something similar to:

```java
PaymentService payment = new PaypalPaymentService();

OrderService orderService = new OrderService(payment);
```

- You never write this code.
- Spring writes it for us.

---

# Container after Injection

```
                 IoC Container

        +---------------------------+
        |   OrderService Bean       |
        |---------------------------|
        | paymentService -----------+---------------+
        +---------------------------+               |
                                                    |
                                                    ▼
                                    +---------------------------+
                                    | PaypalPaymentService Bean |
                                    +---------------------------+
```

Notice
`OrderService`

doesn't know

```java
new PaypalPaymentService()
```

It only knows

```
PaymentService
```

This is called Loose Coupling.

---

# Retrieving the Bean

Then your code says

```java
var orderService = context.getBean(OrderService.class);
```

The IoC container returns the already-created object.

```
Application
      │
      ▼
context.getBean(OrderService.class)
      │
      ▼
IoC Container
      │
      ▼
Returns OrderService Bean
```

No new object is created here.

---

> [!bug]
> Exception in thread "main" org.springframework.beans.factory.NoSuchBeanDefinitionException: No qualifying bean of type 'com.sh.thespringioccontainer.OrderService' available
>
> > ```
> > at org.springframework.beans.factory.support.DefaultListableBeanFactory.getBean(DefaultListableBeanFactory.java:386)
> > at org.springframework.beans.factory.support.DefaultListableBeanFactory.getBean(DefaultListableBeanFactory.java:377>)
> > at org.springframework.context.support.AbstractApplicationContext.getBean(AbstractApplicationContext.java:1317)
> > at com.sh.thespringioccontainer.TheSpringIoCContainerApplication.main(TheSpringIoCContainerApplication.java:12)
> > ```

We fix it later

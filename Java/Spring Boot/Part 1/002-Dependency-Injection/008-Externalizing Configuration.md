# Project Structure

```text
src
 └── main
      ├── java
      │     └── com.sh.externalizingconfiguration
      │              │
      │              ├── ExternalizingConfigurationApplication.java
      │              ├── PaymentService.java
      │              ├── StripePaymentService.java
      │              └── OrderService.java
      │
      └── resources
             └── application.properties
```

---

# 1. PaymentService.java

```java
package com.sh.externalizingconfiguration;

public interface PaymentService {

    void processPayment(double amount);

}
```

---

# 2. StripePaymentService.java

```java
package com.sh.externalizingconfiguration;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
@Primary
public class StripePaymentService implements PaymentService {

    @Value("${stripe.apiUrl}")
    private String apiUrl;

    @Value("${stripe.enabled}")
    private boolean enabled;

    @Value("${stripe.supported-currencies}")
    private List<String> currencies;

    @Override
    public void processPayment(double amount) {

        System.out.println("Stripe Payment");

        System.out.println("Amount : " + amount);
        System.out.println("API URL : " + apiUrl);
        System.out.println("Enabled : " + enabled);
        System.out.println("Currencies : " + currencies);
    }
}
```

---

# 3. OrderService.java

```java
package com.sh.externalizingconfiguration;

import org.springframework.stereotype.Service;

@Service
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

# 4. ExternalizingConfigurationApplication.java

```java
package com.sh.externalizingconfiguration;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class ExternalizingConfigurationApplication {

    public static void main(String[] args) {

        ApplicationContext context =
                SpringApplication.run(ExternalizingConfigurationApplication.class, args);

        OrderService orderService = context.getBean(OrderService.class);

        orderService.placeOrder();

    }

}
```

---

# 5. application.properties

```properties
spring.application.name=ExternalizingConfiguration

stripe.apiUrl=https://api.stripe.com
stripe.enabled=true
stripe.supported-currencies=USD,EUR,GBP
```

---

# Output

```text
Stripe Payment
Amount : 100.0
API URL : https://api.stripe.com
Enabled : true
Currencies : [USD, EUR, GBP]
```

---

# Concept 1: What is Externalized Configuration?

Normally we can write

```java
private String apiUrl = "https://api.stripe.com";
```

- This is called **hardcoding**.
- If tomorrow the URL changes, we must modify the Java code and rebuild the application.

Instead, Spring Boot lets us keep configuration outside the code.

```properties
stripe.apiUrl=https://api.stripe.com
```

Then read it with

```java
@Value("${stripe.apiUrl}")
private String apiUrl;
```

This is called **Externalized Configuration**.

---

# Concept 2: Why do we use it?

Suppose your application runs in three environments.

Development

```text
https://dev-api.stripe.com
```

Testing

```text
https://test-api.stripe.com
```

Production

```text
https://api.stripe.com
```

If the URL is hardcoded

```java
private String apiUrl="https://api.stripe.com";
```

You must edit Java code every time.

Instead

Development

```properties
stripe.apiUrl=https://dev-api.stripe.com
```

Testing

```properties
stripe.apiUrl=https://test-api.stripe.com
```

Production

```properties
stripe.apiUrl=https://api.stripe.com
```

No Java code changes.

Only configuration changes.

---

# Concept 3: What is @Value?

`@Value` reads a property from the configuration file.

Example

```properties
stripe.enabled=true
```

```java
@Value("${stripe.enabled}")
private boolean enabled;
```

Spring automatically injects

```java
enabled = true;
```

---

Another example

```properties
stripe.apiUrl=https://api.stripe.com
```

```java
@Value("${stripe.apiUrl}")
private String apiUrl;
```

becomes

```java
apiUrl = "https://api.stripe.com";
```

---

# Concept 4: Reading List Values

Properties

```properties
stripe.supported-currencies=USD,EUR,GBP
```

Spring automatically converts it into

```java
List<String>
```

using

```java
@Value("${stripe.supported-currencies}")
private List<String> currencies;
```

Result

```java
[USD, EUR, GBP]
```

No conversion code is required.

---

# Concept 5: What happens when the application starts?

Spring Boot reads

```properties
application.properties
```

↓
Finds

```properties
stripe.apiUrl=https://api.stripe.com
```

↓
Creates

```java
StripePaymentService
```

↓
Injects

```java
apiUrl="https://api.stripe.com"
enabled=true
currencies=[USD, EUR, GBP]
```

↓
Your object is ready to use.

---

# Concept 6: Why use application.properties?

Instead of

```java
private boolean enabled=true;

private String apiUrl="https://api.stripe.com";
```

We keep them outside.

Benefits

- No recompilation for configuration changes.
- Different configuration for different environments.
- Sensitive values (API keys, database URLs) stay outside the source code.
- Easier maintenance.

---

# Concept 7: application.properties vs application.yml

Both store the same configuration.

### application.properties

```properties
spring.application.name=ExternalizingConfiguration

stripe.apiUrl=https://api.stripe.com
stripe.enabled=true
stripe.supported-currencies=USD,EUR,GBP
```

### ==application.yaml==

yaml stands for yet another markup language
directory path: resources/application.yaml (make sure, you create it in order to use it)

```yaml
spring:
	application:
		name : ExternalizingConfiguration

stripe:
  apiUrl: https://api.stripe.com
  enabled: true
  supported-currencies:
    - USD
    - EUR
    - GBP
```

Both produce the same values.

YAML is often easier to read because it groups related settings hierarchically.

---

# Concept 8: Other Ways to Externalize Configuration

Besides `application.properties` and `application.yml`, Spring Boot can read configuration from:

| Source                     | Example                                            |
| -------------------------- | -------------------------------------------------- |
| `application.properties`   | `server.port=8080`                                 |
| `application.yml`          | YAML format                                        |
| Environment Variables      | `STRIPE_APIURL=https://api.stripe.com`             |
| JVM System Properties      | `-Dserver.port=9090`                               |
| Command-line Arguments     | `--server.port=9090`                               |
| `@ConfigurationProperties` | Bind a group of related properties to a Java class |

---

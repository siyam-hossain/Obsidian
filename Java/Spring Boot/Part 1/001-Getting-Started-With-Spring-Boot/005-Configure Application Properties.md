- _pom.xml_ #dependencies

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter</artifactId>
	</dependency>

	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
	</dependency>

	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
		<version>4.1.0</version>
	</dependency>
</dependencies>
```

- _application.properties_ #properties

```properties
spring.application.name=ConfigureApplicationProperties
#server.port=8081
app.page-size=10
```

Here,

1. `spring.application.name` consider as key
2. ==ConfigureApplicationProperties== consider as value

- _HomeController.java_ #controller

```java
package com.sh.configureapplicationproperties;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HomeController {

    @Value("${spring.application.name}")
    private String appName;


    @RequestMapping("/")
    public String index(){

        System.out.println("app name: "+appName);

        return "index.html";
    }
}
```

Here,

1. Value annotations: `@Value("${key}")`
2. This key is from ==application.properties==

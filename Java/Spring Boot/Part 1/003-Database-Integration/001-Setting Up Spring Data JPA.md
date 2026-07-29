### Add related starters in pom.xml

1. Open pom.xml
2. Go to dependencies section
3. Add starters (shortcut: `Alt + Insert`)
4. Add `Spring Data JPA`
5. Add `MySQL Driver`

### pom.xml

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
        <artifactId>spring-boot-starter-webmvc</artifactId>
    </dependency>

    <dependency>
	    <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <dependency>
	    <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <scope>runtime</scope>
    </dependency>

</dependencies>
```

### resources/application.yml

```yml
spring:
    application:
        name: SettingSpringDataJPA

    datasource:
        url: jdbc:mysql://localhost:3306/store?createDatabaseIfNotExist=true
        username: root
        password: ''
```

Here,
`store` consider as database name

### To do that

1. attached `flyway-maven` plugin inside pom.xml

```xml
<build>
    <plugins>
	    <plugin>
		    <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

```xml
<build>
    <plugins>
	    <plugin>
		    <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>

        <plugin>
            <groupId>org.flywaydb</groupId>
            <artifactId>flyway-maven-plugin</artifactId>
            <version>12.10.0</version>
            <configuration>
	            <url>jdbc:mysql://localhost:3306/store?createDatabaseIfNotExist=true</url>
                <user>root</user>
                <password></password>
                <cleanDisabled>false</cleanDisabled>
            </configuration>
        </plugin>
    </plugins>
</build>
```

Here,

- Intellij idea some times don't suggest this artifacts
- Rather we can find it from `maven central` website
- `cleanDisabled` to drop entire datable
- To migrate open maven from intellij idea right hand side, sidebar
- Then go to `Plugins` section
- Then open `flyway`
- Then double click on `flyway:migrate`
- `flyway:validate` helps to check is there any database version missing or not
- `flyway:clean` helps to drop the database

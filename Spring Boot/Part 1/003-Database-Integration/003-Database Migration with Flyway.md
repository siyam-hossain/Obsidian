### Add related starters in pom.xml

1.  1. Open `pom.xml`
2.  Go to dependencies section
3.  Add starters (shortcut: `Alt + Insert`)
4.  Add `Spring Data JPA`
5.  Add `MySQL Driver`
6.  Add `Flyway Migration`

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

    <dependency>
	    <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-flyway</artifactId>
    </dependency>

    <dependency>
	    <groupId>org.flywaydb</groupId>
        <artifactId>flyway-mysql</artifactId>
    </dependency>

</dependencies>
```

7. Now add some directories inside resources: `resources/db/migration`
8. Next create a file called: `V1__initial_migration.sql`
   Here, _then convention to write this file is_
    - `V1` always start with capital letter (V1 means version 1)
    - followed by two ( \_ \_ ) lines `__`
    - then description name
    - ends with `.sql`

### Database versioning

| generate `sql` script                                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------ |
| ![Database Integration](https://raw.githubusercontent.com/siyam-hossain/images/main/Spring%20Boot/Part%201/Database%20Integration/008.png) |
| Copy `sql` script                                                                                                                          |
| ![Database Integration](https://raw.githubusercontent.com/siyam-hossain/images/main/Spring%20Boot/Part%201/Database%20Integration/009.png) |
| paste it into `V1__initial_migration.sql`                                                                                                  |

```sql
create table users
(
    id       bigint auto_increment
        primary key,
    name     varchar(255) not null,
    email    varchar(255) not null,
    password varchar(255) not null
);

create table addresses
(
    id      bigint auto_increment
        primary key,
    street  varchar(255) not null,
    city    varchar(255) not null,
    zip     varchar(255) not null,
    user_id bigint       not null,
    constraint addresses_users_id_fk
        foreign key (user_id) references users (id)
);
```

| drop the database                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![Database Integration](https://raw.githubusercontent.com/siyam-hossain/images/main/Spring%20Boot/Part%201/Database%20Integration/010.png)                         |
| Note: to drop this database the localhost database must run in background in port 3306 otherwise you won't drop the database                                       |
| Now rerun the application                                                                                                                                          |
| ![Database Integration](https://raw.githubusercontent.com/siyam-hossain/images/main/Spring%20Boot/Part%201/Database%20Integration/011.png)                         |
| It creates an additional table inside database along with other 2 tables, `flyway_schema_history` track the database version so that same thing is not implemented |

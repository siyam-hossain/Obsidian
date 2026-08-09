This is a **JPA Entity class**. It represents a **`users` table** in your database. Spring Data JPA uses this class to map Java objects to database rows.

Let's go through it line by line.

---

## Package

We need to create a package inside the application package called `entities`

```java
package com.database.settingspringdatajpa.entities;
```

This simply tells Java that the `User` class belongs to the `entities` package.

---

## Import Statements

We don't need to write it explicitly, but it can be written in automatically while we use `@Entity` annotation.

```java
import jakarta.persistence.*;
```

Imports all JPA annotations like:

- `@Entity`
- `@Table`
- `@Id`
- `@GeneratedValue`
- `@Column`

These annotations tell Spring Boot how this class maps to a database table.

---

## @Entity

```java
@Entity
```

Marks this class as a **JPA Entity**.
Without this annotation, Spring Boot treats it as a normal Java class.

Example:

```java
@Entity
public class User {
}
```

means:

> "This class represents a table in the database."

---

## @Table

```java
@Table(name="users")
```

Specifies the database table name.

Without it:

```java
@Entity
public class User {
}
```

Spring automatically looks for a table named

```
user
```

(or `User`, depending on the naming strategy).

With

```java
@Table(name="users")
```

Spring will use

```
users
```

instead.

---

## Primary Key

```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```

### `@Id`

Marks this field as the **Primary Key**.

Database:

| id  | username |
| --- | -------- |
| 1   | John     |
| 2   | Alice    |

`id` uniquely identifies every user.

---

### `@GeneratedValue`

```java
@GeneratedValue(strategy = GenerationType.IDENTITY)
```

Tells the database to generate the ID automatically.

Example:

```java
User user = new User();
user.setUsername("John");
```

You **do not** do:

```java
user.setId(1L);
```

When saved:

```java
repository.save(user);
```

Database automatically creates

```
id = 1
```

Next insert:

```
id = 2
```

Next:

```
id = 3
```

This usually maps to MySQL's:

```sql
AUTO_INCREMENT
```

---

## Username Column

```java
@Column(nullable = false, name = "name")
private String username;
```

This maps

```java
private String username;
```

to the database column

```
name
```

Notice:

Java field:

```java
username
```

Database column:

```sql
name
```

Example table:

| id  | name |
| --- | ---- |
| 1   | John |

In Java:

```java
user.getUsername();
```

returns

```
John
```

---

### `nullable = false`

Means this column **cannot be NULL**.
SQL generated is similar to

```sql
name VARCHAR(255) NOT NULL
```

Trying to save

```java
user.setUsername(null);
```

will cause a database error.

---

## Email

```java
@Column(nullable = false, name = "email")
private String email;
```

Maps

```java
email
```

to database column

```
email
```

Generated SQL is similar to

```sql
email VARCHAR(255) NOT NULL
```

---

## Password

```java
@Column(nullable = false, name = "password")
private String password;
```

Maps

```java
password
```

to

```
password
```

Also cannot be `NULL`.

---

## Getters

Example:

```java
public String getUsername() {
    return username;
}
```

Used to read the value.

Example:

```java
User user = new User();

String name = user.getUsername();
```

---

## Setters

Example:

```java
public void setUsername(String username) {
    this.username = username;
}
```

Used to assign a value.

Example:

```java
User user = new User();

user.setUsername("Siyam");
```

Now

```java
user.getUsername();
```

returns

```
Siyam
```

---

# What table will this create?

If Hibernate is configured to generate the schema, it will create something similar to:

```sql
CREATE TABLE users (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    password VARCHAR(255) NOT NULL
);
```

Notice that the Java field `username` is stored in the **`name`** column because of:

```java
@Column(name = "name")
private String username;
```

---

# Example of saving a user

```java
User user = new User();

user.setUsername("Siyam");
user.setEmail("siyam@gmail.com");
user.setPassword("123456");

userRepository.save(user);
```

After saving, the database will contain:

| id  | name  | email                                     | password |
| --- | ----- | ----------------------------------------- | -------- |
| 1   | Siyam | [siyam@gmail.com](mailto:siyam@gmail.com) | 123456   |

---

## Summary

| Annotation                                            | Purpose                                                    |
| ----------------------------------------------------- | ---------------------------------------------------------- |
| `@Entity`                                             | Marks the class as a JPA entity (database table).          |
| `@Table(name = "users")`                              | Maps the entity to the `users` table.                      |
| `@Id`                                                 | Marks the primary key.                                     |
| `@GeneratedValue(strategy = GenerationType.IDENTITY)` | Lets the database auto-generate the ID (`AUTO_INCREMENT`). |
| `@Column(name = "...")`                               | Maps a Java field to a specific database column.           |
| `nullable = false`                                    | Prevents `NULL` values in that column.                     |
| Getters                                               | Read field values.                                         |
| Setters                                               | Modify field values.                                       |

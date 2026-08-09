### For Bi-directional

![Database Integration](https://raw.githubusercontent.com/siyam-hossain/images/main/Spring%20Boot/Part%201/Database%20Integration/023.png)

## User Entity (`User.java`)

```java
package com.database.settingspringdatajpa.entities;

import jakarta.persistence.*;
import lombok.*;

import java.util.ArrayList;
import java.util.List;

@ToString
@Setter
@Getter
@AllArgsConstructor
@NoArgsConstructor
@Builder
@Entity
@Table(name="users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @Column(name = "name")
    private String username;

    @Column(name = "email")
    private String email;

    @Column(name = "password")
    private String password;

    // A user can have many addresses
    @OneToMany(mappedBy = "user")
    @Builder.Default
    private List<Address> addresses = new ArrayList<>();

    // Wire both objects together
    public void addAddress(Address address) {
        addresses.add(address);
        address.setUser(this);
    }

    public void removeAddress(Address address) {
        addresses.remove(address);
        address.setUser(null);
    }
}
```

### `@OneToMany(mappedBy = "user")`

```java
@OneToMany(mappedBy = "user")
private List<Address> addresses = new ArrayList<>();
```

**Why it was added:**

Defines a **one-to-many** relationship where one `User` can have multiple `Address` objects. The `mappedBy = "user"` indicates that the `user` field in the `Address` entity owns the relationship.

**Advantage:**

- Represents one user with multiple addresses.
- Avoids creating an unnecessary join table.
- Keeps the relationship synchronized through the owning side (`Address`).

---

### `@Builder.Default`

```java
@Builder.Default
private List<Address> addresses = new ArrayList<>();
```

**Why it was added:**

Ensures the `addresses` list is initialized when creating a `User` using Lombok's Builder.

**Advantage:**

- Prevents `addresses` from being `null`.
- Allows addresses to be added immediately after object creation.
- Preserves the default value when using `User.builder().build()`.

---

### `addAddress()`

```java
public void addAddress(Address address) {
    addresses.add(address);
    address.setUser(this);
}
```

**Why it was added:**
Adds an address to the user's address list and simultaneously assigns the current user to that address.

**Advantage:**

- Keeps both sides of the bidirectional relationship synchronized.
- Prevents inconsistent object references.
- Only one method call is needed to establish the relationship.

---

### `removeAddress()`

```java
public void removeAddress(Address address) {
    addresses.remove(address);
    address.setUser(null);
}
```

**Why it was added:**
Removes an address from the user's address list and clears its associated user.

**Advantage:**

- Keeps both sides of the relationship synchronized.
- Prevents stale or incorrect references.
- Makes relationship removal simple and consistent.

---

---

## Address Entity (`Address.java`)

```java
package com.database.settingspringdatajpa.entities;

import jakarta.persistence.*;
import lombok.*;

@ToString
@Getter
@Setter
@Builder
@AllArgsConstructor
@NoArgsConstructor
@Entity
@Table(name = "addresses")
public class Address {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private long id;

    @Column(nullable = false, name = "street")
    private String street;

    @Column(nullable = false, name = "city")
    private String city;

    @Column(nullable = false, name = "zip")
    private String zip;

    @Column(nullable = false, name = "state")
    private String state;

    @ManyToOne
    @JoinColumn(name = "user_id")
    @ToString.Exclude
    private User user;

}
```

### `@ManyToOne`

```java
@ManyToOne
@JoinColumn(name = "user_id")
private User user;
```

**Why it was added:**
Defines the **many-to-one** side of the relationship. Each `Address` belongs to a single `User`. The `user_id` column acts as the foreign key.

**Advantage:**

- Establishes the foreign key relationship.
- Allows an address to access its associated user.
- This is the owning side responsible for updating the database relationship.

---

### `@ToString.Exclude`

```java
@ToString.Exclude
private User user;
```

**Why it was added:**
Excludes the `user` field from the generated `toString()` method.

**Advantage:**

- Prevents infinite recursive calls when printing objects.
- Avoids `StackOverflowError` in bidirectional relationships.
- Produces cleaner and more readable output.

---

---

## Main Class

```java
package com.database.settingspringdatajpa;

import com.database.settingspringdatajpa.entities.Address;
import com.database.settingspringdatajpa.entities.User;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class SettingSpringDataJpaApplication {

    public static void main(String[] args) {
//        SpringApplication.run(SettingSpringDataJpaApplication.class, args);

        var user = User.builder()
                .username("admin")
                .password("admin")
                .email("admin@gmail.com")
                .build();

        var address = Address.builder()
                .street("123 Main St")
                .city("Main St")
                .state("Main St")
                .zip("12345")
                .build();

        user.addAddress(address);
        System.out.println(user);

        user.removeAddress(address);
        System.out.println(user);

    }
}
```

---

## Bidirectional Relationship

```
User (1)
   │
   │ One-to-Many
   ▼
Address (Many)

User ---------> List<Address>
  ▲                 │
  └─────────────────┘
        Address.user
```

**Advantage of a Bidirectional Relationship:**

- A `User` can access all of its `Address` objects.
- An `Address` can directly access its owning `User`.
- Both entities remain synchronized, making navigation and data access possible from either side.

---

---

## `Address` is the owner of the relationship

### Why?

Because it contains the `@JoinColumn` annotation:

```java
@ManyToOne
@JoinColumn(name = "user_id")
private User user;
```

The entity that has `@JoinColumn` is called the **owning side** because it manages the foreign key (`user_id`) in the database.

---

### Non-owning (Inverse) Side

```java
@OneToMany(mappedBy = "user")
private List<Address> addresses = new ArrayList<>();
```

The `mappedBy = "user"` tells JPA:

> "Don't create or manage the foreign key here. The `user` field in the `Address` entity already owns this relationship."

So, **`User` is the inverse (non-owning) side**.

---

## Database Representation

```text
users
+----+-------+
| id | name  |
+----+-------+
|  1 | Admin |
+----+-------+

addresses
+----+-------------+---------+
| id | street      | user_id |
+----+-------------+---------+
|  1 | 123 Main St |    1    |
|  2 | Park Road   |    1    |
+----+-------------+---------+
```

Notice that the foreign key **`user_id`** exists in the **`addresses`** table, not in the `users` table. Therefore, `Address` owns the relationship.

---

## Summary

| Entity    | Role                          | Reason                                                                                                |
| --------- | ----------------------------- | ----------------------------------------------------------------------------------------------------- |
| `Address` | **Owning Side**               | Contains `@ManyToOne` and `@JoinColumn`, manages the `user_id` foreign key.                           |
| `User`    | **Inverse (Non-owning) Side** | Uses `@OneToMany(mappedBy = "user")`, references the owning side but does not manage the foreign key. |

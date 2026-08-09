## For Bi-directional Many to Many

![Database Integration](https://raw.githubusercontent.com/siyam-hossain/images/main/Spring%20Boot/Part%201/Database%20Integration/024.png)

---

## User Entity (`User.java`)

```java
package com.database.settingspringdatajpa.entities;

import jakarta.persistence.*;
import lombok.*;

import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Set;

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
    // A user not necessary know about address
    @Builder.Default
    // we are telling the builder to include the below statement or initialization when building an object
    private List<Address> addresses = new ArrayList<>();

    // let's wire the objects together
    public void addAddress(Address address) {
        addresses.add(address);
        address.setUser(this);
    }

    public void removeAddress(Address address) {
        addresses.remove(address);
        address.setUser(null);
    }

    public void addTag(String tagName) {
        var tag = new Tag(tagName);
        tags.add(tag);
        tag.getUser().add(this);
    }

    public void removeTag(String tagName) {
        var tag = new Tag(tagName);
        tags.remove(tag);
        tag.getUser().remove(this);
    }

    // a user can't have duplicate tags
    // for many-to-many relationship either part can be owner
    // for many-to-many relationship we use join-table instead of join-column
    @ManyToMany
    @JoinTable(
            name = "user_tags",
            // foreign key of current table which is present on table: "user_tags"
            joinColumns = @JoinColumn(name = "user_id"),
            inverseJoinColumns = @JoinColumn(name = "tag_id")
    )

    @Builder.Default
    private Set<Tag> tags = new HashSet<>();
}
```

---

# 1. `@ManyToMany`

```java
@ManyToMany
```

### Why it is written

Declares a **Many-to-Many** relationship between `User` and `Tag`.

- One **User** can have multiple **Tag** objects.
- One **Tag** can belong to multiple **User** objects.

### Advantage

- Models many-to-many relationships directly.
- JPA automatically manages the relationship.

---

# 2. `@JoinTable`

```java
@JoinTable(
        name = "user_tags",
        joinColumns = @JoinColumn(name = "user_id"),
        inverseJoinColumns = @JoinColumn(name = "tag_id")
)
```

### Why it is written

Creates a join table named **`user_tags`** to store the relationship.
It will look like:

| user_id | tag_id |
| ------- | ------ |
| 1       | 1      |
| 1       | 2      |
| 2       | 1      |

### Explanation

```java
name = "user_tags"
```

Creates the join table.

---

```java
joinColumns = @JoinColumn(name = "user_id")
```

Represents the foreign key referencing the **User** table.

---

```java
inverseJoinColumns = @JoinColumn(name = "tag_id")
```

Represents the foreign key referencing the **Tag** table.

### Advantage

- No extra entity is needed for the relationship.
- JPA automatically inserts and removes records from the join table.

---

# 3. `Set<Tag>`

```java
@Builder.Default
private Set<Tag> tags = new HashSet<>();
```

### Why it is written

Stores all tags associated with the current user.
A **Set** is used instead of a **List** because duplicate tags are not allowed.

### Advantage

- Prevents duplicate tags.
- Automatically initialized when using the Builder.

---

# 4. `addTag()`

```java
public void addTag(String tagName) {
    var tag = new Tag(tagName);
    tags.add(tag);
    tag.getUser().add(this);
}
```

### Why it is written

Creates a tag and **wires both objects together**.

### Step-by-step

#### Step 1

```java
var tag = new Tag(tagName);
```

Creates a new `Tag`.

```
Tag

name = "Java"

users = []
```

---

#### Step 2

```java
tags.add(tag);
```

Adds the tag to the current user's tag collection.

```
User

tags

↓

Java
```

At this point, **only the User knows about the Tag**.

---

#### Step 3

```java
tag.getUser().add(this);
```

Let's break it down.

```java
tag.getUser()
```

Returns

```java
Set<User>
```

because inside `Tag` there is

```java
private Set<User> user;
```

Then

```java
.add(this)
```

adds the **current User object**.

`this`
means

> the current `User` object that called `addTag()`.

After execution:

```
User ─────► Tag
 ▲          │
 └──────────┘
```

Now both objects know each other.

### Advantage

- Keeps both sides synchronized.
- Prevents inconsistent object references.
- One method call establishes the relationship completely.

---

# 5. `removeTag()`

```java
public void removeTag(String tagName) {
    var tag = new Tag(tagName);
    tags.remove(tag);
    tag.getUser().remove(this);
}
```

### Why it is written

Removes the relationship from both sides.

### Step-by-step

```java
tags.remove(tag);
```

Removes the tag from the user's collection.

---

```java
tag.getUser().remove(this);
```

Removes the user from the tag's collection.

Before:

```
User ⇄ Java
```

After:

```
User      Java
```

The relationship is removed from both sides.

### Advantage

- Keeps the object graph synchronized.
- Prevents stale references.
- Makes relationship removal simple and consistent.

---

---

## Tag Entity (`Tag.java`)

```java
package com.database.settingspringdatajpa.entities;

import jakarta.persistence.*;
import lombok.*;

import java.util.HashSet;
import java.util.Set;

@AllArgsConstructor
@NoArgsConstructor
@ToString
@Getter
@Setter
@Entity
@Table(name = "tags")
public class Tag {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Integer id;

    @Column(name = "name")
    private String name;

    // the "tags" comes form User entity Set--->tags
    @ManyToMany(mappedBy = "tags")
    @ToString.Exclude
    private Set<User> user = new HashSet<>();

    public Tag(String name) {
        this.name = name;
    }
}
```

---

# 1. `@ManyToMany(mappedBy = "tags")`

```java
@ManyToMany(mappedBy = "tags")
```

### Why it is written

Declares the **inverse (non-owning)** side of the Many-to-Many relationship.
The `mappedBy` attribute tells JPA that the relationship is already managed by the `tags` field in the `User` entity.

It refers to this field in `User.java`:

```java
private Set<Tag> tags = new HashSet<>();
```

This tells JPA:

> "Do not create another join table. Use the relationship already defined in the `User` entity."

### Advantage

- Prevents JPA from creating two join tables.
- Allows a `Tag` to access all associated `User` objects.
- Keeps the relationship bidirectional.

---

# 2. `@ToString.Exclude`

```java
@ToString.Exclude
private Set<User> user = new HashSet<>();
```

### Why it is written

Excludes the `user` collection from Lombok's generated `toString()` method.
Without this annotation, printing a `User` or `Tag` object causes infinite recursion.

Example:

```text
User
 └── Tag
      └── User
            └── Tag
                  └── User
                        ...
```

Eventually, the application throws a **StackOverflowError**.

### Advantage

- Prevents infinite recursive printing.
- Produces cleaner console output.
- Avoids `StackOverflowError`.

---

# 3. `private Set<User> user = new HashSet<>();`

```java
private Set<User> user = new HashSet<>();
```

### Why it is written

Stores all users associated with the current tag.

Example:

```text
Java
│
├── Admin
├── John
└── Alice
```

Here, the **Java** tag belongs to three users.
A `Set` is used because duplicate users are not allowed.

### Advantage

- Stores multiple users for a single tag.
- Prevents duplicate users.
- Provides fast lookup and removal operations.

---

# 4. Constructor

```java
public Tag(String name) {
    this.name = name;
}
```

### Why it is written

Creates a `Tag` object by providing only its name.

Example:

```java
var tag = new Tag("Java");
```

Instead of writing:

```java
var tag = new Tag();
tag.setName("Java");
```

### Advantage

- Makes object creation shorter and cleaner.
- Useful when only the tag name is needed.
- Reduces boilerplate code.

---

## Relationship Diagram

```text
                User (Owner)
                     │
                     │ @ManyToMany
                     ▼
               user_tags (Join Table)
              +---------+--------+
              | user_id | tag_id |
              +---------+--------+
                     ▲
                     │
                     │ @ManyToMany(mappedBy = "tags")
                     │
                Tag (Inverse Side)
```

### Summary

| Code                             | Purpose                                           | Advantage                                                            |
| -------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------- |
| `@ManyToMany(mappedBy = "tags")` | Declares the inverse side of the relationship.    | Prevents duplicate join tables and enables bidirectional navigation. |
| `@ToString.Exclude`              | Excludes the `user` collection from `toString()`. | Prevents infinite recursion and `StackOverflowError`.                |
| `Set<User>`                      | Stores all users associated with a tag.           | Prevents duplicates and supports efficient collection operations.    |
| `Tag(String name)`               | Creates a tag using only its name.                | Simplifies object creation and reduces boilerplate.                  |

---

---

## Main Class (`SettingSpringDataJpaApplication.java`)

```java
package com.database.settingspringdatajpa;

import com.database.settingspringdatajpa.entities.Address;
import com.database.settingspringdatajpa.entities.Tag;
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

        user.addTag("tag 1");

        System.out.println(user);
    }
}
```

---

# 1. Creating a `User` Object

```java
var user = User.builder()
        .username("admin")
        .password("admin")
        .email("admin@gmail.com")
        .build();
```

### Why it is written

Creates a new `User` object using Lombok's **Builder Pattern**.

The generated object contains:

```text
User
----------------------
username = admin
email = admin@gmail.com
password = admin
tags = []
```

### Advantage

- Creates objects in a clean and readable way.
- Only the required fields need to be specified.
- Avoids calling multiple setter methods.

---

# 2. Adding a Tag

```java
user.addTag("tag 1");
```

### Why it is written

Calls the `addTag()` helper method to create a `Tag` object and establish the relationship between the `User` and the `Tag`.

Internally, this executes:

```java
var tag = new Tag("tag 1");

tags.add(tag);

tag.getUser().add(this);
```

### Step-by-Step

**Step 1**

Creates a new tag.

```text
Tag

name = "tag 1"

users = []
```

---

**Step 2**

```java
tags.add(tag);
```

Adds the tag to the user's collection.

```text
User

tags
↓

[tag 1]
```

At this point, only the **User** knows about the **Tag**.

---

**Step 3**

```java
tag.getUser().add(this);
```

Adds the current `User` to the tag's `user` collection.

After execution:

```text
User
 │
 ▼
Tag

▲
│

User
```

Now both objects know about each other. This is called **wiring the relationship**.

### Advantage

- Synchronizes both sides of the bidirectional relationship.
- Prevents inconsistent object references.
- Encapsulates the relationship logic in a single helper method.

---

# 3. Printing the User

```java
System.out.println(user);
```

### Why it is written

Prints the `User` object along with its associated tags.

Example output (simplified):

```text
User(
    id=null,
    username=admin,
    email=admin@gmail.com,
    password=admin,
    tags=[Tag(id=null, name=tag 1)]
)
```

Since `Tag.user` is annotated with `@ToString.Exclude`, the `user` collection inside `Tag` is not printed.

### Advantage

- Displays the established relationship.
- Avoids infinite recursion while printing.
- Makes debugging easier.

---

## Execution Flow

```text
Create User
      │
      ▼
user.addTag("tag 1")
      │
      ▼
Create Tag
      │
      ▼
User.tags.add(tag)
      │
      ▼
Tag.users.add(user)
      │
      ▼
Relationship Wired
      │
      ▼
Print User
```

### Result

After execution, the object graph looks like this:

```text
User (admin)
     │
     ▼
Tag (tag 1)
     ▲
     │
     └────────── User (admin)
```

This bidirectional reference allows:

- A **User** to access all its **Tag** objects.
- A **Tag** to access all its associated **User** objects.

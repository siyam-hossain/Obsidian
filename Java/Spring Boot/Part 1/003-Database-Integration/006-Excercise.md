![Database Integration](https://raw.githubusercontent.com/siyam-hossain/images/main/Spring%20Boot/Part%201/Database%20Integration/020.png)

`V4__add_profiles_table.sql`

```sql
CREATE TABLE profiles(
    id BIGINT PRIMARY KEY,
    bio TEXT,
    phone_number VARCHAR(15),
    date_of_birth DATE,
    loyalty_point INT UNSIGNED Default 0,
    FOREIGN KEY (id) references users(id)
);
```

`V5__add_tags_table.sql`

```sql
CREATE TABLE tags(
     id INT AUTO_INCREMENT PRIMARY KEY,
     name VARCHAR(255) NOT NULL
);

CREATE TABLE user_tags(
      user_id BIGINT NOT NULL,
      tag_id INT NOT NULL,

      PRIMARY KEY (user_id, tag_id),

      FOREIGN KEY (user_id)
          REFERENCES users(id)
          ON DELETE CASCADE,

      FOREIGN KEY (tag_id)
          REFERENCES tags(id)
          ON DELETE CASCADE
);
```

Then just the migration from : `flyway:migrate`

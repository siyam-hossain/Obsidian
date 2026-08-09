# Dart operators

## Arithmetic Operators in Dart

Arithmetic operators are used to perform **mathematical operations**.

| Operator | Name                | Example   |     Result |
| -------- | ------------------- | --------- | ---------: |
| `+`      | Addition            | `10 + 3`  |       `13` |
| `-`      | Subtraction         | `10 - 3`  |        `7` |
| `*`      | Multiplication      | `10 * 3`  |       `30` |
| `/`      | Division            | `10 / 3`  | `3.333...` |
| `~/`     | Integer Division    | `10 ~/ 3` |        `3` |
| `%`      | Modulus (Remainder) | `10 % 3`  |        `1` |

### Example

```dart
void main() {
  int a = 10;
  int b = 3;

  print(a + b);   // 13
  print(a - b);   // 7
  print(a * b);   // 30
  print(a / b);   // 3.3333333333333335
  print(a ~/ b);  // 3
  print(a % b);   // 1
}
```

```output
13
7
30
3.3333333333333335
3
1
```

**Note:** `/` returns a `double`, while `~/` performs integer division and returns an `int`.

---

## Unary Operators in Dart

**Unary operators** operate on **one operand** (one value).

| Operator | Name           | Example | Result                  |
| -------- | -------------- | ------- | ----------------------- |
| `++`     | Increment      | `++x`   | Increases `x` by 1      |
| `--`     | Decrement      | `--x`   | Decreases `x` by 1      |
| `-`      | Unary Minus    | `-x`    | Changes sign of `x`     |
| `!`      | Logical NOT    | `!true` | `false`                 |
| `~`      | Bitwise NOT    | `~x`    | Inverts bits            |
| `!`      | Null Assertion | `x!`    | Asserts `x` is non-null |

### Example

```dart
void main() {
  int x = 10;

  print(++x); // 11
  print(--x); // 10
  print(-x);  // -10

  bool value = true;
  print(!value); // false
}
```

```output
11
10
-10
false
```

### Pre vs Post Increment

```dart
int x = 5;

print(++x); // 6 → increment first
print(x++); // 6 → use first, then increment
print(x);   // 7
```

```output
6
6
7
```

**In short:** Unary operators work with **only one operand**.

---

## Assignment Operators in Dart

Assignment operators are used to **assign or update values** in variables.

| Operator | Name                    | Example    | Equivalent                         |
| -------- | ----------------------- | ---------- | ---------------------------------- |
| `=`      | Assignment              | `x = 10`   | `x = 10`                           |
| `+=`     | Add & Assign            | `x += 5`   | `x = x + 5`                        |
| `-=`     | Subtract & Assign       | `x -= 5`   | `x = x - 5`                        |
| `*=`     | Multiply & Assign       | `x *= 5`   | `x = x * 5`                        |
| `/=`     | Divide & Assign         | `x /= 5`   | `x = x / 5`                        |
| `~/=`    | Integer Divide & Assign | `x ~/= 5`  | `x = x ~/ 5`                       |
| `%=`     | Modulus & Assign        | `x %= 5`   | `x = x % 5`                        |
| `??=`    | Assign if Null          | `x ??= 10` | Assigns `10` only if `x` is `null` |

### Example

```dart
void main() {
  int x = 10;

  x += 5;
  print(x);

  x -= 3;
  print(x);

  x *= 2;
  print(x);

  x ~/= 4;
  print(x);
}
```

```output
15
12
24
6
```

### Null-Aware Assignment

```dart
void main() {
  String? name;

  name ??= "Siyam";

  print(name);
}
```

```output
Siyam
```

`??=` assigns a value **only when the variable is `null`**.

---

## Relational Operators in Dart

Relational operators are used to **compare two values**. The result is always a **`bool`** (`true` or `false`).

| Operator | Name                     | Example    | Result  |
| -------- | ------------------------ | ---------- | ------- |
| `(==)`   | Equal to                 | `10 == 10` | `true`  |
| `!=`     | Not equal to             | `10 != 5`  | `true`  |
| `>`      | Greater than             | `10 > 5`   | `true`  |
| `<`      | Less than                | `10 < 5`   | `false` |
| `>=`     | Greater than or equal to | `10 >= 10` | `true`  |
| `<=`     | Less than or equal to    | `10 <= 5`  | `false` |

### Example

```dart
void main() {
  int a = 10;
  int b = 5;

  print(a == b);
  print(a != b);
  print(a > b);
  print(a < b);
  print(a >= b);
  print(a <= b);
}
```

```ouput
false
true
true
false
true
false
```

**Note:** Relational operators are mainly used in **conditions**, such as `if`, `while`, and `for` statements.

---

## Type Test / Type Casting Operators in Dart

| Operator | Description                              | Example        |
| -------- | ---------------------------------------- | -------------- |
| `is`     | Checks whether a value is a type         | `x is int`     |
| `is!`    | Checks whether a value is **not** a type | `x is! String` |
| `as`     | Typecasts a value to a specific type     | `x as String`  |

### `as` Operator

The `as` operator is used to **cast a value to a specific type**.

```dart
void main() {
  dynamic value = "Siyam";

  String name = value as String;

  print(name);
}
```

```output
Siyam
```

```dart
void main() {
  var x = 10;
  var name = "Siyam";

  print(x is int);
  print(x is String);

  print(name is String);
  print(name is! int);
}
```

```output
true
false
true
true
```

### Difference

```dart
value is String
```

➡️ **Checks** if `value` is a `String`.

```dart
value as String
```

➡️ **Treats/casts** `value` as a `String`.

So, for documentation, you can write:

---

## Bitwise Operators in Dart

Bitwise operators perform operations on the **individual bits** of integer values.

| Operator | Name                 | Example   | Result |
| -------- | -------------------- | --------- | -----: |
| `&`      | Bitwise AND          | `5 & 3`   |    `1` |
| `\|`     | Bitwise OR           | `5 \| 3`  |    `7` |
| `^`      | Bitwise XOR          | `5 ^ 3`   |    `6` |
| `~`      | Bitwise NOT          | `~5`      |   `-6` |
| `<<`     | Left Shift           | `5 << 1`  |   `10` |
| `>>`     | Right Shift          | `5 >> 1`  |    `2` |
| `>>>`    | Unsigned Right Shift | `5 >>> 1` |    `2` |

### Example

```dart
void main() {
  int a = 5; // 0101
  int b = 3; // 0011

  print(a & b);  // 0001 = 1
  print(a | b);  // 0111 = 7
  print(a ^ b);  // 0110 = 6
  print(~a);     // -6
  print(a << 1); // 1010 = 10
  print(a >> 1); // 0010 = 2
}
```

```output
1
7
6
-6
10
2
```

### Quick Understanding

For `5 & 3`:

```text
  0101  (5)
& 0011  (3)
------
  0001  (1)
```

**Note:** Bitwise operators are mainly useful when working with **binary data, flags, masks, embedded systems, and low-level programming**.

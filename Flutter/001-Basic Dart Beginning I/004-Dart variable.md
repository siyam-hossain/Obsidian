**Variable is used to store the value and refer the memory location in computer memory.**

- The variable cannot contain special characters such as whitespace, mathematical symbol, runes, Unicode character, and keywords.
- The first character of the variable should be an alphabet. Digits are not allowed as the first character.
- Variables are case sensitive. For example, variable age and AGE are treated differently.
- The special character such as `#, @, ^, &, *` are not allowed expect the underscore `(_)` and the dollar sign `($)`.
- The variable name should be retable to the program and readable.

---

```dart
void main(){
  var x = 10;
  var y = 23;
  var z = x+y;

  print(x);
  print(y);
  print(z);
}
```

```output
10
23
33
```

---

# Dart data types

```text
Dart Types
│
├── Numbers
│   ├── int
│   ├── double
│   └── num
│
├── Text
│   └── String
│
├── Boolean
│   └── bool
│
├── Collections
│   ├── List
│   ├── Set
│   └── Map
│
├── Functions
│   └── Function
│
└── Other
    ├── Record
    ├── Object
    ├── dynamic
    └── Null
```

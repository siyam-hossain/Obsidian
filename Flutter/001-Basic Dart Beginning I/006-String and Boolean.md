# Dart String

1. A string is the sequence of the character. If we store the data - name, address, special character, etc.
2. It is signified by using either sing quotes or double quotes.

```dart
void main(){
  var myCountry = "My country name is Bangladesh";
  var name = 'Siyam Hossain';

  print(myCountry);
  print(myCountry.runtimeType);
  print(name);
  print(name.runtimeType);
}
```

```output
My country name is Bangladesh
String
Siyam Hossain
String
```

---

# Dart Boolean

- The Boolean type represents the two values : true and false
- The `bool` keyword uses to denote Boolean Type.
- The numeric values 1 and 0 cannot be used to represent the true or false value.

```dart
void main(){
  var positive = true;
  var negative = false;

  print(positive);
  print(negative);

  print(positive.runtimeType);
  print(negative.runtimeType);
}
```

```output
true
false
bool
bool
```

---

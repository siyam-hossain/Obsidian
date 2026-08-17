# Dart Abstract Classes

- Abstract classes are the classes in Dart that has one or more abstract method.
- Abstraction is a part of the data encapsulation where the actual internal working of the function hides from the users.
- They interact only with external functionality.
- We can declare the abstract class by using the `abstract` keyword.
- There is a possibility that an abstract class may or may not have abstract methods.

---

`Father.dart` abstract class.

- If we don't want users to create objects directly from a class, we can make that class `abstract`.
- An abstract class is mainly used when the class represents a **general concept** and you don't want it to be instantiated directly.

```dart
abstract class Father {
  fathersMoney();
}
```

`Son.dart`

```dart
import 'Father.dart';

class Son extends Father{

  @override
  fathersMoney() {
    print("Money: 20000000");
  }
}
```

`Main.dart`

```dart
import 'Son.dart';

void main() {

  var sonObj = Son();
  sonObj.fathersMoney();

}
```

```output
Money: 20000000
```

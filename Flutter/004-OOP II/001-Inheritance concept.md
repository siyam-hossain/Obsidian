# Dart inheritance

1. Dart inheritance is defined as the process of deriving the properties and characteristics of another class.
2. It provides the ability to create a new class from an existing class.
3. It is the most essential concept of the oops.
4. We can reuse the all the behavior and characteristics of the previous class in the new class.

# Parent class

A class which is inherited by the other class is called superclass or parent class. It is also known as a base class.

# Child class

A class which inherits properties from other class is called the child class. It is also known as the derived class or subclass.

---

`Father.dart`

```dart
class Father {
  fathersMoney(){
    print("Total amount of father: 8000000");
  }
}
```

`Son.dart`

```dart
import 'Father.dart';

class Son extends Father{

}
```

`Main.dart`

```dart
import 'Father.dart';
import 'Son.dart';

void main() {

  var fatherObj = Father();
  fatherObj.fathersMoney();

  var sonObj = Son();
  sonObj.fathersMoney();

}
```

```output
Total amount of father: 8000000
Total amount of father: 8000000
```

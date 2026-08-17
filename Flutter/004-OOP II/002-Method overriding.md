# Method Overriding

- When we declare the same method in the subclass, which is previously defined in the superclass is known as the method overriding.
- The subclass can define the same method by providing its own implementation, which is already exists in the superclass.
- The method in the superclass is called method overridden, and method in the subclass is called method overriding.

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
  //Son can override fathersMoney method
  @override
  fathersMoney() {
    // TODO: implement fathersMoney
    print("Son increase father money 2X");
  }
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
Son increase father money 2X
```

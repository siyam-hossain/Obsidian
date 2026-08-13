Note:

- Properties (fields/attributes) are defined inside a class.
- Instance properties belong to individual objects (instances) of that class.
- Each object gets its own separate copy of those instance properties

`MyClass.dart`

```dart
class MyClass{
  var myName = "siyam hossain";
  var myList = ['a','b','c'];

  addTwoNumber(int x, int y){
    print("x+y: ${x+y}");
  }

  addThreeNumber(int x, int y, int z){
    print("x+y+z: ${x+y+z}");
  }
}
```

`Main.dart`

```dart
import 'MyClass.dart';

void main() {
  var object = MyClass();
  object.addTwoNumber(10, 45);
  object.addThreeNumber(10, 20, 30);

  print(object.myName);
  print(object.myList);
  print(object.myList[0]);

}
```

```output
x+y: 55
x+y+z: 60
siyam hossain
[a, b, c]
a
```

---

# Static

In Dart, `static` means a member belongs to the class itself rather than to each individual object.

```dart
class MyClass{
  static var myName = "siyam hossain";
  static var myList = ['a','b','c'];

  static addTwoNumber(int x, int y){
    print("x+y: ${x+y}");
  }

  static addThreeNumber(int x, int y, int z){
    print("x+y+z: ${x+y+z}");
  }
}
```

Without creating an object, we can access a class's static methods or properties using the class name. The `static` keyword makes the member belong to the class itself rather than to individual objects.

```dart
import 'MyClass.dart';

void main() {

  MyClass.addTwoNumber(10, 45);
  MyClass.addThreeNumber(10, 20, 30);

  print(MyClass.myName);
  print(MyClass.myList);
  print(MyClass.myList[0]);

}
```

```output
x+y: 55
x+y+z: 60
siyam hossain
[a, b, c]
a
```

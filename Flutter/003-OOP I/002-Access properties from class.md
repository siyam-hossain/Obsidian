# Accessing variable & function from class

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

void main() {
  var object = new MyClass();
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

# Class in different file

External class file name

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

Then import this class where you want to use it.

```dart
import 'MyClass.dart';

void main() {
  var object = new MyClass();
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

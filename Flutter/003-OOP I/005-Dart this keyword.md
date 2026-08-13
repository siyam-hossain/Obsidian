# Dart this keyword

1. The this keyword is used to refer the current class object.
2. It indicates the current instance of the class, methods, or constructor.

```dart
class MyClass{

  var num1 = 11;
  var num2 = 23;

  addTwoNumber(){
    print(this.num1 + this.num2);
  }

  myFunction(){
    this.addTwoNumber();
  }

}
```

```dart
import 'MyClass.dart';

void main() {

  var obj = MyClass();
  obj.myFunction();

}
```

```output
34
```

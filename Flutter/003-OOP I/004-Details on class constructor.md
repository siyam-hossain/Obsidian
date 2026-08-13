# Class constructor

A constructor is a different type of function which is created with same name as its class name. The constructor is used to initialize an object when it is created.

1. Constructor has no return type
2. Constructor can have parameter
3. Constructor execute automatically

Class with `default` constructor

```dart
class MyClass{
  MyClass(){
    print("This is a constructor");
  }
}
```

```dart
import 'MyClass.dart';

void main() {

  var obj = MyClass();

}
```

```output
This is a constructor
```

---

# Constructor with parameter

```dart
class MyClass{
  MyClass(String msg){
    print(msg);
  }
}
```

```dart
import 'MyClass.dart';

void main() {

  var obj = MyClass("This is a constructor");

}
```

```output
This is a constructor
```

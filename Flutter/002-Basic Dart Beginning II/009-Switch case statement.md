# Switch case statement

1. Dart switch case statement is used to avoid the long chain of the if-else statement.
2. It is the simplified form if nested if-else statement.

```dart
import 'dart:io';
void main() {

  print("Enter your marks: ");
  var marks = int.parse(stdin.readLineSync()!);

  if(marks <= 100 && marks>=0){
    switch(marks){
      case >= 80:
        print("A+");
        break;

      case >= 70:
        print("A");
        break;

      case >= 60:
        print("A-");
        break;

      case >= 50:
        print("B");
        break;

      case >= 40:
        print("C");
        break;

      default:
        print("fail");
        break;
    }
  }else{
    print("Invalid marks");
  }

}
```

```output
Enter your marks:
39
fail
```

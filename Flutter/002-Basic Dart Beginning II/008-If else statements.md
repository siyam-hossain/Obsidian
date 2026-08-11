# If statement

If statement allows us to a block of code execute when the given condition returns true.

```dart
import 'dart:io';
void main() {

  print("Enter your marks: ");
  var marks = int.parse(stdin.readLineSync()!);

  if(marks>=80){
    print("A+");
  }

}
```

```output
Enter your marks:
20

Enter your marks:
90
A+
```

---

# If else statements

In dart, if block is executed when the given condition is true. If the given condition is false, else block is executed.

```dart
import 'dart:io';
void main() {

  print("Enter your marks: ");
  var marks = int.parse(stdin.readLineSync()!);

  if(marks>=80){
    print("A+");
  }
  else{
    print("Result is below A+");
  }

}
```

```output
Enter your marks:
79
Result is below A+
```

---

# If else-if statement

1. Dart if else-if statement provides the facility to check a set of test expressions and execute the different statements.
2. It is used when we have to make a decision from more than two possibilities.

```dart
import 'dart:io';
void main() {

  print("Enter your marks: ");
  var marks = int.parse(stdin.readLineSync()!);

  if(marks<=100 && marks>=80){
    print("A+");
  }
  else if(marks >= 70){
    print("A");
  }
  else if(marks >= 60){
    print("A-");
  }
  else if(marks >= 50){
    print("B");
  }
  else if(marks >= 40){
    print("C");
  }
  else{
    print("Fail");
  }

}
```

```output
Enter your marks:
70
A
```

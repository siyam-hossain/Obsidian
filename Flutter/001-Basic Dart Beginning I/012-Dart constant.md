# Dart constant

**Dart constant is defined as an immutable object**

- Which means it can't be changed or modified during the execution of the program.
- Once we initialize the value to the constant variable, it cannot be reassigned later.

**The dart constant can be defined in the following two ways.**

- Using the final keyword
- Using the const key

```dart
void main() {
  final pi = 3.1416;
  // pi = pi + 1;
  print(pi);


  const PI = 3.1416;
  // PI = PI + 1;
  print(PI);

}
```

```output
3.1416
3.1416
```

```dart
void main() {
  final pi = 3.1416;
  pi = pi + 1;
  print(pi);
}
```

> [!bug]
> Error: Can't assign to the final variable 'pi'.
> pi = pi + 1;
> ^^

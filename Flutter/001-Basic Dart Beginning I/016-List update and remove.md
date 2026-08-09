# Updating List

We want to update specific value of a list.

```dart
void main() {
  var numbers = [1, 2, 3, 4, 5];
  print(numbers);

  numbers[1] = 255;
  print(numbers);
}
```

```output
[1, 2, 3, 4, 5]
[1, 255, 3, 4, 5]
```

---

# Remove from list

If we want to remove last element from the list.

```dart
void main() {
  var numbers = [1, 2, 3, 4, 5];
  print(numbers);

  numbers.removeLast();
  print(numbers);
}
```

```output
[1, 2, 3, 4, 5]
[1, 2, 3, 4]
```

If we want to remove from a specific index.

```dart
void main() {
  var numbers = [1, 65, 3, 4, 5];
  print(numbers);

  numbers.removeAt(1);
  print(numbers);
}
```

```output
[1, 65, 3, 4, 5]
[1, 3, 4, 5]
```

If we want to remove range based

```dart
void main() {
  var numbers = [1, 65, 3, 45, 5];
  print(numbers);

  numbers.removeRange(0,4);
  print(numbers);
}
```

```output
[1, 65, 3, 45, 5]
[5]
```

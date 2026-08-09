# List properties

#### List Properties in Dart

A `List` is an **ordered collection** of values. Dart provides many useful properties and methods for working with lists.

#### Common List Properties

| Property     | Description                                      | Example           |
| ------------ | ------------------------------------------------ | ----------------- |
| `length`     | Returns number of elements                       | `list.length`     |
| `isEmpty`    | Checks if list is empty                          | `list.isEmpty`    |
| `isNotEmpty` | Checks if list is not empty                      | `list.isNotEmpty` |
| `first`      | Returns first element                            | `list.first`      |
| `last`       | Returns last element                             | `list.last`       |
| `reversed`   | Returns elements in reverse order                | `list.reversed`   |
| `single`     | Returns the only element if list has exactly one | `list.single`     |

#### Example

```dart
void main() {
  List<int> numbers = [10, 20, 30, 40];

  print(numbers.length);
  print(numbers.isEmpty);
  print(numbers.isNotEmpty);
  print(numbers.first);
  print(numbers.last);
  print(numbers.reversed);
}
```

```output
4
false
true
10
40
(40, 30, 20, 10)
```

```dart
void main() {
  var numbers = [10, 20, 30, "siyam"];

  print(numbers.length);
  print(numbers.isEmpty);
  print(numbers.isNotEmpty);
  print(numbers.first);
  print(numbers.last);
  print(numbers.reversed);
}
```

```output
4
false
true
10
siyam
(siyam, 30, 20, 10)
```

#### Important

`first` and `last` are properties:

```dart
numbers.first
numbers.last
```

While things like `add()`, `remove()`, and `contains()` are **methods**, not properties.

# Dart Lists

- The list is a collection of the ordered objects (value). The concept of list is similar to an array.
- An array is defined as a collection of the multiple elements in single variable.
- The elements in the list are separated by the comma enclosed in the square bracket `[]`.

```dart
void main(){
  var list = [1, 2, 3];
  var name = ['siyam', 'hossain', 'sh'];
  var mixed = ['siyam', 1, 3.1416, true];

  print(list[0]);
  print(list.runtimeType);

  print(name[1]);
  print(name.runtimeType);

  print(mixed[3]);
  print(mixed.runtimeType);
}
```

```output
1
List<int>
hossain
List<String>
true
List<Object>
```

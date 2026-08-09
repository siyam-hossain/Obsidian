# Dart maps

- The maps type is used to store values in key-value pairs. Each key is associated with its value.
- The key and value can be any type. In Map, the key must be unique, but a value can occur multiple times.
- The map is defined by using curly braces `{}` , and comma separates each pair.

```dart
void main(){
  var student = {
    "name" : "siyam hossain",
    "age" : 23,
    "dept" : "CSE"
  };

  print(student["name"]);
  print(student["age"]);
  print(student["dept"]);
}
```

```output
siyam hossain
23
CSE
```

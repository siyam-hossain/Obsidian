# Adding value at runtime

To declare a Map using map literal, the key-value pairs are enclosed within the curly braces `{}` and separated by the commas.

```dart
void main() {
  var person = {
    'name' : 'siyam hossain',
    'age' : 21,
    'city' : 'Dhaka'
  };
  print(person);

  // adding additional element
  person['country'] = 'Bangladesh';
  print(person);
}
```

```output
{name: siyam hossain, age: 21, city: Dhaka}
{name: siyam hossain, age: 21, city: Dhaka, country: Bangladesh}
```

---

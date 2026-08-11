# allAll()

It adds multiple key-value pairs of other. the syntax is given below.

```dart
void main() {
  var person = {
    'name' : 'siyam hossain',
    'age' : 21,
    'city' : 'Dhaka'
  };
  print(person);

  person.addAll(
    {
      'country' : 'Bangladesh',
      'blood-group' : 'B+'
    }
  );
  print(person);

}
```

```output
{name: siyam hossain, age: 21, city: Dhaka}
{name: siyam hossain, age: 21, city: Dhaka, country: Bangladesh, blood-group: B+}
```

---

# clear()

It eliminates all pairs from the map.

```dart
void main() {
  var person = {
    'name' : 'siyam hossain',
    'age' : 21,
    'city' : 'Dhaka'
  };
  print(person);

  person.clear();

  print(person);

}
```

```output
{name: siyam hossain, age: 21, city: Dhaka}
{}
```

---

# remove()

It removes the key and its associated value if it exists in the given map.

```dart
void main() {
  var person = {
    'name' : 'siyam hossain',
    'age' : 21,
    'city' : 'Dhaka'
  };
  print(person);

  person.remove('city');

  print(person);

}
```

```output
{name: siyam hossain, age: 21, city: Dhaka}
{name: siyam hossain, age: 21}
```

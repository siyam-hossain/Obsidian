# Map constructor

- To declare the Dart Map using map constructor can be done in two ways.
- First, declare a map using map() constructor. Second, initialize the map.

```dart
void main() {

  var person = new Map();
  person['name'] = 'Siyam';
  person['age'] = 23;
  person['city'] = 'Dhaka';
  person['country'] = 'Bangladesh';

  print(person);
}
```

```output
{name: Siyam, age: 23, city: Dhaka, country: Bangladesh}
```

---

# Map properties

| Properties | Explanation                                                     |
| ---------- | --------------------------------------------------------------- |
| Keys       | It is used to get all keys as an iterable object.               |
| values     | It is used to get all values as an iterable object.             |
| Length     | It returns the length of the Map object.                        |
| isEmpty    | If the map object contains no value, it returns true.           |
| isNotEmpty | If the map object contains at least one value, it returns true. |

```dart
void main() {

  var person = new Map();
  person['name'] = 'Siyam';
  person['age'] = 23;
  person['city'] = 'Dhaka';
  person['country'] = 'Bangladesh';

  print(person);
  print("keys: ${person.keys}");
  print("values: ${person.values}");
  print("length: ${person.length}");
  print("is empty: ${person.isEmpty}");
  print("is not empty: ${person.isNotEmpty}");

}
```

```output
{name: Siyam, age: 23, city: Dhaka, country: Bangladesh}
keys: (name, age, city, country)
values: (Siyam, 23, Dhaka, Bangladesh)
length: 4
is empty: false
is not empty: true
```

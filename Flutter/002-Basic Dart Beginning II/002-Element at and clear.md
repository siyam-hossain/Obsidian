# Access the set element

Dart provides the `elementAt()` method, which is used to access the item by passing its specified index position.

```dart
void main() {

  var myCitySet = <String>{'Dhaka', 'Chandpur', 'Comilla'};
  myCitySet.add('Sylhet');

  myCitySet.addAll(
    {'Barisal', 'Jessore'}
  );

  print(
    myCitySet.elementAt(2)
  );
}
```

```output
Comilla
```

---

# Clear

We can remove entire set element by using the clear methods.

```cpp
void main() {

  var myCitySet = <String>{'Dhaka', 'Chandpur', 'Comilla'};
  myCitySet.add('Sylhet');

  myCitySet.addAll(
    {'Barisal', 'Jessore'}
  );

  print(myCitySet);
  myCitySet.clear();
  print(myCitySet);
}
```

```output
{Dhaka, Chandpur, Comilla, Sylhet, Barisal, Jessore}
{}
```

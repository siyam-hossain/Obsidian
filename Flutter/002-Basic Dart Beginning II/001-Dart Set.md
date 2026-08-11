# Dart set

- The dart set is the unordered collection of the **different** values of the **same type**.
- It has much functionality, which is the same as an array, but it is unordered.
- Set doesn't allow storing the **duplicated** values.
- Set must contain unique values.

```dart
void main() {

  var myCitySet = <String>{'Dhaka', 'Chandpur', 'Comilla'};
  print(myCitySet);

}
```

```output
{Dhaka, Chandpur, Comilla}
```

Here,
`<String>` is the generics or type conversion.

---

# Add element into set

The dart provides the two methods `add()` and `addAll()` to insert an element into the given set.

```cpp
void main() {

  var myCitySet = <String>{'Dhaka', 'Chandpur', 'Comilla'};
  print(myCitySet);

  myCitySet.add('Sylhet');
  print(myCitySet);

  myCitySet.addAll(
    {'Barisal', 'Jessore'}
  );
  print(myCitySet);
}
```

```output
{Dhaka, Chandpur, Comilla}
{Dhaka, Chandpur, Comilla, Sylhet}
{Dhaka, Chandpur, Comilla, Sylhet, Barisal, Jessore}
```

---

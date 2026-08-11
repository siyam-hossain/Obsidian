# Set properties

| Properties | Explanations                                                 |
| ---------- | ------------------------------------------------------------ |
| first      | It is used to get the first element in the given set.        |
| isEmpty    | If the set does not contain any element, it returns true.    |
| isNotEmpty | If the set contains at least one element, it returns true.   |
| length     | It returns the length of the given set.                      |
| last       | It is used to get the last element in the given set.         |
| hashcode   | It is used to get the hash code for the corresponding object |
| Single     | It is used to check whether a set contains only one element. |

```dart
void main() {

  var myCitySet = <String>{'Dhaka', 'Chandpur', 'Comilla'};
  myCitySet.add('Sylhet');

  myCitySet.addAll(
    {'Barisal', 'Jessore'}
  );

  print(myCitySet.first);
  print(myCitySet.last);
  print(myCitySet.isEmpty);
  print(myCitySet.isNotEmpty);
  print(myCitySet.length);
  print(myCitySet.hashCode);
}
```

```output
Dhaka
Jessore
false
true
6
1040605280
```

---

```dart
void main() {
  var myCitySet = <String>{'Dhaka', 'Chandpur', 'Comilla'};
  myCitySet.add('Sylhet');

  myCitySet.addAll(
      {'Barisal', 'Jessore'}
  );
  try{
    print(myCitySet.single);
  }catch (e){
    //if myCitySet contain more than one element
    print("Error: ${e}");
  }
}
```

```output
Error: Bad state: Too many elements
```

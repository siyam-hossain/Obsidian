# List Insert

Data provides four methods which are used to insert the elements into the lists. These methods are given below.

- add()
- addAll()
- insert()
- insertAll()

##### add()

Add an element at the end of the list.

```dart
void main() {
  var myList = [1, 2, 3, 4, 5];
  print(myList);

  myList.add(65);
  print(myList);
}
```

```output
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5, 65]
```

##### addAll()

Add elements at the end of the list.

```dart
void main() {
  var myList = [1, 2, 3, 4, 5];
  print(myList);

  myList.addAll([6,7,6,9,8]);
  print(myList);
}
```

```output
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5, 6, 7, 6, 9, 8]
```

##### insert()

Add an element at the specific index which is present.

```dart
void main() {
  var myList = [1, 2, 3, 4, 5];
  print(myList);

  myList.insert(2,65);
  print(myList);
}
```

```output
[1, 2, 3, 4, 5]
[1, 2, 65, 3, 4, 5]
```

##### insertAll()

Add all element at the specific index which is present.

```dart
void main() {
  var myList = [1, 2, 8, 4, 5];
  print(myList);

  myList.insertAll(3,[65,9,100]);
  print(myList);
}
```

```output
[1, 2, 8, 4, 5]
[1, 2, 8, 65, 9, 100, 4, 5]
```

---

##### Issues

```dart
void main() {
  var myList = [1, 2, 8, 4, 5];
  print(myList);

  myList.insertAll(6,[65,9,100]);
  print(myList);
}
```

> [!bug]
>
> ```
> Unhandled exception:
> RangeError: Invalid value: Not in inclusive range 0..5: 6
> #0      List.insertAll (dart:core-patch/growable_array.dart:44:7)
> #1      main (file:///D:/Rat_Race/Flutter/001-Getting-Started/001-Hello-World/hello_world/bin/hello_world.dart:5:10)
> #2      _delayEntrypointInvocation.<anonymous closure> (dart:isolate-patch/isolate_patch.dart:313:19)
> #3      _RawReceivePort._handleMessage (dart:isolate-patch/isolate_patch.dart:192:12)
> ```

```text
this happens due to 6 is not a valid index
```

```dart
void main() {
  var myList = [1, 2, 8, 4, 5];
  print(myList);

  myList.insertAll(3,[65,9,100,'true', 3.14]);
  print(myList);
}
```

> [!bug] Type Error
>
> ```text
> bin/hello_world.dart:5:32: Error: A value of type 'String' can't be assigned to a variable of type 'int'.
> myList.insertAll(3, [65, 9, 100, 'true', 3.14]);
>                                ^
>
> bin/hello_world.dart:5:40: Error: A value of type 'double' can't be assigned to a variable of type 'int'.
> myList.insertAll(3, [65, 9, 100, 'true', 3.14]);
>                                          ^
>
> Process finished with exit code 254
> ```

```text
This can't insert different datatype into it
cause list type is `int`
```

```dart
void main() {
  var myList = [1, 2, 8, 4, 5, 'true'];
  print(myList);

  myList.insertAll(3,[65,9,100,'true', 3.14]);
  print(myList);
}
```

```output
[1, 2, 8, 4, 5, true]
[1, 2, 8, 65, 9, 100, true, 3.14, 4, 5, true]
```

```text
Now this is possible cause the list type is `object`
```

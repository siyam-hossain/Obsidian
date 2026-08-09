# Fixed length list

- The fixed length lists are defined with the specified length.
- We cannot change the size at runtime.

```dart
void main() {
  const myList = [1, 2, 3, 4, 5];
  print(myList);
}
```

```output
[1, 2, 3, 4, 5]
```

```dart
void main() {
  const myList = [1, 2, 3, 4, 5];
  print(myList);

  myList.add(65);
  print(myList);
}
```

> [!bug] Unhandled Exception
>
> ```text
> Unhandled exception: Unsupported operation: Cannot add to an unmodifiable list.
> #0      UnmodifiableListMixin.add (dart:internal/list.dart:112:5)
> #1      main (file:///D:/Rat_Race/Flutter/001-Getting-Started/001-Hello-World/hello_world/bin/hello_world.dart:5:10)
> #2      _delayEntrypointInvocation.<anonymous closure> (dart:isolate-patch/isolate_patch.dart:313:19)
> #3      _RawReceivePort._handleMessage (dart:isolate-patch/isolate_patch.dart:192:12)
> [1, 2, 3, 4, 5]
> ```

---

# Growable List

- The list declared without specifying size is known as a Grow able list.
- The size of the Grow able list can be modified at the runtime.

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

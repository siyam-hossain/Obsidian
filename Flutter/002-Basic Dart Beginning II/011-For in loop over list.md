# Dart for...in loop over list

The for...in loop is slightly different from the for lop. It only takes dart object or expression as an iterator and iterates the element one at a time.

```dart
void main() {

  var myList = [1,2,3,4,true, 'siyam', 2.4];

  for(var item in myList){
    print("list element: $item");
  }

}
```

```output
list element: 1
list element: 2
list element: 3
list element: 4
list element: true
list element: siyam
list element: 2.4
```

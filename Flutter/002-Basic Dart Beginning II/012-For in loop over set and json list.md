# For in loop over set

```dart
void main() {

  var mySet = {1,2,3,4,5,6,7,8,9,10};

  for(var item in mySet){
    print("set element: $item");
  }

}
```

```output
set element: 1
set element: 2
set element: 3
set element: 4
set element: 5
set element: 6
set element: 7
set element: 8
set element: 9
set element: 10
```

---

# For in loop over json list

```dart
void main() {

  //json format of data
  var productList = [
    {'name' : 'soap', 'price' : 180}, //object
    {'name' : 'tee', 'price' : 65},
    {'name' : 'speed', 'price' : 30},
    {'name' : 'mojo', 'price' : 20},
    {'name' : 'sugar', 'price' : 105},
    {'name' : 'chips', 'price' : 15},

  ];//list

  for(var oneProduct in productList){
    print("-------------------------------");
    print("product: $oneProduct");
    print("name: ${oneProduct['name']}");
    print("price: ${oneProduct['price']}");
  }
  print("-------------------------------");

}
```

```ouput
-------------------------------
product: {name: soap, price: 180}
name: soap
price: 180
-------------------------------
product: {name: tee, price: 65}
name: tee
price: 65
-------------------------------
product: {name: speed, price: 30}
name: speed
price: 30
-------------------------------
product: {name: mojo, price: 20}
name: mojo
price: 20
-------------------------------
product: {name: sugar, price: 105}
name: sugar
price: 105
-------------------------------
product: {name: chips, price: 15}
name: chips
price: 15
-------------------------------
```

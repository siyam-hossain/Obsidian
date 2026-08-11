# Function parts

##### return_type

It can be any data type such as `void`, `integer`, `float`, etc. The return type must be matched with the returned value of the function.

##### func_name

It should be an appropriate and valid identifier.

##### parameter_list

It denotes the list of the parameters, which is necessary when we called a function.

##### return value

A function returns a value after complete its execution.

---

# Define a function

- A function can be defined by providing the name of the function with the appropriate parameter and return type.
- A function contains a set of statements which are called function body.

```dart
void addTwoNumber(){
  int x = 6;
  int y = 75;
  print("sum: ${x+y}");
}
void main() {

}
```

```output

```

---

# Calling a function

After creating a function, we can call or invoke the defined function inside the main() function body.

```dart
void addTwoNumber(){
  int x = 6;
  int y = 75;
  print("sum: ${x+y}");
}
void main() {
  addTwoNumber();
}
```

```output
sum: 81
```

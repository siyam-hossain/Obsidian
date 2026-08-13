# Function return & return type

- It can be any data type such as void, integer, float, etc. The return type must be matched with the returned value of the function
- A function returns a value after complete its execution.

```dart
int addTwoNumber(int x, int y){
  return x+y;
}
void main() {
  int res = addTwoNumber(25, 46);
  print("Result: $res");
}
```

```output
Result: 71
```

---

# Main function

- The main() function is the top level function of the dart.
- It is the most important and vital function of the dart programming language.
- It execution of the programming starts with the main() function.
- The main() function can be used only once in a program.

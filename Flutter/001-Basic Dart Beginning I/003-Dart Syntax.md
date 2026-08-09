# Dart Syntax

**Syntax is called set of rules for writing programs. Dart has-**

- Variables and operators
- Classes
- Functions
- Expressions and programming constructs
- Decision making and looping constructs
- Comments
- Libraries and packages
- Data structures represented as Collections / Generics

#### Whitespace and line breaks

Dart ignores spaces, tabs, and newlines that appear in programs.

#### Dart in Case-sensitive

Dart is case-sensitive. This means that dart differentiates between uppercase and lowercase characters.

#### Statements end with a semicolon

Each line of instruction is called a statement. Each dart statement must end with a semicolon.

#### Comments in dart

Single-line comments `(//)` Multi-line comments `/**/`

---

# Dart Keywords

| Category                          | Keywords                                                                                              |
| --------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **Variables & Types**             | `var`, `final`, `const`, `late`, `dynamic`, `void`, `Object`, `Null`                                  |
| **Classes & Objects**             | `class`, `extends`, `implements`, `with`, `mixin`, `abstract`, `interface`, `base`, `sealed`, `final` |
| **Functions**                     | `return`, `async`, `await`, `sync`, `yield`, `external`                                               |
| **Control Flow**                  | `if`, `else`, `switch`, `case`, `default`, `for`, `while`, `do`, `break`, `continue`                  |
| **Error Handling**                | `try`, `catch`, `finally`, `throw`, `rethrow`, `on`, `assert`                                         |
| **Constructors & Initialization** | `this`, `super`, `new`, `factory`, `required`                                                         |
| **Imports & Libraries**           | `import`, `export`, `library`, `part`, `show`, `hide`, `deferred`, `as`                               |
| **Access & Operators**            | `is`, `is!`, `in`, `operator`                                                                         |
| **Enums & Extensions**            | `enum`, `extension`, `extension type`                                                                 |
| **Other**                         | `typedef`, `get`, `set`, `covariant`, `required`                                                      |

---

#### Example

```dart
void main(){

  // single line comment
  /*    Multi-line comment  */

  const x = 3;
  const X = "siyam hossain";

  print("Hello world");
  print("x: ${x}");
  print("X: $X");
}
```

```output
Hello world
x: 3
X: siyam hossain
```

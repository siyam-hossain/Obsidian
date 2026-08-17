# Material App class

MaterialApp is a predefined class in a flutter. Main or core component of flutter.

- `Color`: It controls the primary color used in the application.
- `darkTheme`: It provide theme data for the dark theme for the application.
- `debugShowCheckedModeBanner`: This property takes in a Boolean as the object to decide whether to show the debug banner or not.
- `home`: This property takes in widget as the object to show on the default route of the app.

```dart
class MyApp extends StatelessWidget {

  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {

    return MaterialApp(

      theme: ThemeData(primaryColor: Colors.green),
      darkTheme: ThemeData(primaryColor: Colors.blue),
      color: Colors.blue,
      debugShowCheckedModeBanner: false,
      home: HomeActivity(),
    );
  }

}
```

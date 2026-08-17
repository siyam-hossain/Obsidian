# Flutter AppBar Widget

AppBar is usually the topmost component of the app. It contains the toolbar and some other common action buttons.

- `actions`: This property takes in a list of widgets as a parameter to be displayed after the title if the `AppBar` is a row.
- `title`: This property usually takes in the main widget as a parameter to be displayed in the AppBar.
- `backgroundColor`: This property is used to add colors to the background of the `AppBar`
- `elevation`: This property is used to set the z-coordinate at which to place this app bar relative to its parent.

```dart
class HomeActivity extends StatelessWidget {

  const HomeActivity({super.key});



  @override

  Widget build(BuildContext context) {

    return Scaffold(

      appBar: AppBar(

        title: Text("Inventory App"),

        titleSpacing: 0,

        centerTitle: true,

        toolbarHeight: 60,

        toolbarOpacity: 1,

        elevation: 0,

        backgroundColor: Colors.green,

        foregroundColor: Colors.white,

      ),

    );

  }

}
```

```dart
class HomeActivity extends StatelessWidget {

  const HomeActivity({super.key});



  @override

  Widget build(BuildContext context) {

    return Scaffold(

      appBar: AppBar(

        title: Text("Inventory App"),

        titleSpacing: 10,

        centerTitle: false,

        toolbarHeight: 60,

        toolbarOpacity: 1,

        elevation: 0,

        backgroundColor: Colors.green,

        foregroundColor: Colors.white,



        actions: [

          IconButton(onPressed: () {}, icon: Icon(Icons.comment)),

          IconButton(onPressed: () {}, icon: Icon(Icons.search)),

          IconButton(onPressed: () {}, icon: Icon(Icons.settings)),

          IconButton(onPressed: () {}, icon: Icon(Icons.email)),

        ],

      ),

    );

  }

}
```

```dart
import 'package:flutter/material.dart';



void main() {

  runApp(const MyApp());

}



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



class HomeActivity extends StatelessWidget {

  const HomeActivity({super.key});



  void mySnackBar(String message, BuildContext context) {

    ScaffoldMessenger.of(context).showSnackBar(

      SnackBar(backgroundColor: Colors.green, content: Text(message)),

    );

  }



  @override

  Widget build(BuildContext context) {

    return Scaffold(

      appBar: AppBar(

        title: Text("Inventory App"),

        titleSpacing: 10,

        centerTitle: false,

        toolbarHeight: 60,

        toolbarOpacity: 1,

        elevation: 0,

        backgroundColor: Colors.green,

        foregroundColor: Colors.white,



        actions: [

          IconButton(

            onPressed: () {

              mySnackBar("Comments", context);

            },

            icon: Icon(Icons.comment),

          ),

          IconButton(

            onPressed: () {

              mySnackBar("Search", context);

            },

            icon: Icon(Icons.search),

          ),

          IconButton(

            onPressed: () {

              mySnackBar("Settings", context);

            },

            icon: Icon(Icons.settings),

          ),

          IconButton(

            onPressed: () {

              mySnackBar("Email", context);

            },

            icon: Icon(Icons.email),

          ),

        ],

      ),

    );

  }

}
```

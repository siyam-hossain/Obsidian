```dart
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



      floatingActionButton: FloatingActionButton(

        backgroundColor: Colors.green,

        foregroundColor: Colors.white,

        elevation: 10,

        shape: const CircleBorder(),

        onPressed: () {

          mySnackBar("This is a floating action button", context);

        },

        child: Icon(Icons.add),

      ),

    );

  }

}
```

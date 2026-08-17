# Simple Form

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

    ButtonStyle buttonStyle = ElevatedButton.styleFrom(

      minimumSize: Size(double.infinity, 60),

    );



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

      ),



      body: Column(

        mainAxisAlignment: MainAxisAlignment.start,

        children: [

          Padding(

            padding: EdgeInsets.all(20),

            child: TextField(

              decoration: InputDecoration(

                border: OutlineInputBorder(),

                label: Text("First Name"),

              ),

            ),

          ),

          Padding(

            padding: EdgeInsets.all(20),

            child: TextField(

              decoration: InputDecoration(

                border: OutlineInputBorder(),

                label: Text("Last Name"),

              ),

            ),

          ),

          Padding(

            padding: EdgeInsets.all(20),

            child: TextField(

              decoration: InputDecoration(

                border: OutlineInputBorder(),

                label: Text("Email Address"),

              ),

            ),

          ),

          Padding(

            padding: EdgeInsets.all(20),

            child: ElevatedButton(

              onPressed: () {},

              style: buttonStyle,

              child: Text("Submit"),

            ),

          ),

        ],

      ),

    );

  }

}
```

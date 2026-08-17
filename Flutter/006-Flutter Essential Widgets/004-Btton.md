# Flutter Button

- Elevated Button
- Text Button
- Outline Button

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

      padding: EdgeInsets.all(15),

      backgroundColor: Colors.green,

      foregroundColor: Colors.white,

      shape: RoundedRectangleBorder(

        borderRadius: BorderRadius.all(Radius.circular(50)),

      ),

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



      body: Padding(

        padding: EdgeInsets.only(top: 20),



        child: Row(

          mainAxisAlignment: MainAxisAlignment.spaceEvenly,

          children: [

            TextButton(

              onPressed: () {

                mySnackBar("Text Button", context);

              },

              child: Text("Text Button"),

            ),



            ElevatedButton(

              onPressed: () {

                mySnackBar("Elevated Button", context);

              },

              style: buttonStyle,

              child: Text("Elevated Button"),

            ),



            OutlinedButton(

              onPressed: () {

                mySnackBar("Outline Button", context);

              },

              child: Text("Outline Button"),

            ),

          ],

        ),

      ),

    );

  }

}
```

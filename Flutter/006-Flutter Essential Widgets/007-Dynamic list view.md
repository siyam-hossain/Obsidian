# List View Builder From Array

Step 01: Json Array
Step 02: List View Builder
Step 03: Gesture Detector
Step 04: List item
Step 05: List Item On Tap/On Press

```dart
class HomeActivity extends StatelessWidget {

  HomeActivity({super.key});



  void mySnackBar(String message, BuildContext context) {

    ScaffoldMessenger.of(context).showSnackBar(

      SnackBar(backgroundColor: Colors.red, content: Text(message)),

    );

  }



  var myItems = [

    {

      "img": "https://raw.githubusercontent.com/siyam-hossain/images/refs/heads/main/Flutter/006-Flutter%20Essential%20Widgets/007-banner.png",

      "title": "Hossian",

    },

    {

      "img": "https://raw.githubusercontent.com/siyam-hossain/images/refs/heads/main/Flutter/006-Flutter%20Essential%20Widgets/007-banner.png",

      "title": "Hossian",

    },

    {

      "img": "https://raw.githubusercontent.com/siyam-hossain/images/refs/heads/main/Flutter/006-Flutter%20Essential%20Widgets/007-banner.png",

      "title": "Hossian",

    },

    {

      "img": "https://raw.githubusercontent.com/siyam-hossain/images/refs/heads/main/Flutter/006-Flutter%20Essential%20Widgets/007-banner.png",

      "title": "Hossian",

    },

    {

      "img": "https://raw.githubusercontent.com/siyam-hossain/images/refs/heads/main/Flutter/006-Flutter%20Essential%20Widgets/007-banner.png",

      "title": "Hossian",

    },

    {

      "img": "https://raw.githubusercontent.com/siyam-hossain/images/refs/heads/main/Flutter/006-Flutter%20Essential%20Widgets/007-banner.png",

      "title": "Hossian",

    },

  ];



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

        backgroundColor: Colors.red,

        foregroundColor: Colors.white,

      ),



      body: ListView.builder(

        itemCount: myItems.length,

        itemBuilder: (context, index) {

          return GestureDetector(

            onTap: () {

              mySnackBar(myItems[index]['title']!, context);

            },

            child: Container(

              margin: EdgeInsets.all(10),

              width: double.infinity,

              height: 200,

              child: Image.network(myItems[index]['img']!, fit: BoxFit.fill),

            ),

          );

        },

      ),

    );

  }

}
```

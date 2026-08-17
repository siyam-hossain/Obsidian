# Grid View Builder From Array

Step 01: Json array
Step 02: Grid view builder
Step 03: Gesture detector
Step 04: Grid Item
Step 05: Grid item on Tap

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



      body: GridView.builder(

        gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(

          crossAxisCount: 2,

          crossAxisSpacing: 0,

          childAspectRatio: 1.2,

        ),

        itemCount: myItems.length,

        itemBuilder: (context, index) {

          return GestureDetector(

            onTap: () {

              mySnackBar(myItems[index]['title']!, context);

            },

            child: Container(

              margin: EdgeInsets.all(5),

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

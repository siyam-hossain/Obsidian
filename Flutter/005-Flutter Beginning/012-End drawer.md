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



      bottomNavigationBar: BottomNavigationBar(

        type: BottomNavigationBarType.fixed,

        currentIndex: 1,

        items: [

          BottomNavigationBarItem(icon: Icon(Icons.home), label: "Home"),

          BottomNavigationBarItem(icon: Icon(Icons.message), label: "Contact"),

          BottomNavigationBarItem(icon: Icon(Icons.person), label: "Profile"),

          // CHANGE 2: Added additional icon item (Settings)

          BottomNavigationBarItem(

            icon: Icon(Icons.settings),

            label: "Settings",

          ),

        ],

        onTap: (int index) {

          if (index == 0) {

            mySnackBar("Home", context);

          }

          if (index == 1) {

            mySnackBar("Contact", context);

          }

          if (index == 2) {

            mySnackBar("Profile", context);

          }

          if (index == 3) {

            mySnackBar("Settings", context);

          }

        },

      ),



      endDrawer: Drawer(

        child: ListView(

          children: [

            DrawerHeader(

              padding: EdgeInsets.all(0),

              child: UserAccountsDrawerHeader(

                decoration: BoxDecoration(color: Colors.green),



                currentAccountPicture: Image.network(

                  "https://github.com/siyam-hossain.png",

                ),



                accountName: Padding(

                  padding: const EdgeInsets.only(top: 10.0),

                  child: Text(

                    "Siyam Hossain",

                    style: TextStyle(color: Colors.black),

                  ),

                ),



                accountEmail: Text(

                  "siyam.cybersoul@gmail.com",

                  style: TextStyle(color: Colors.black),

                ),

              ),

            ),

            ListTile(

              leading: Icon(Icons.home),

              title: Text("Home"),

              onTap: () {

                mySnackBar("Home", context);

              },

            ),

            ListTile(

              leading: Icon(Icons.contact_mail),

              title: Text("Contact"),

              onTap: () {

                mySnackBar("Contact", context);

              },

            ),

            ListTile(

              leading: Icon(Icons.person),

              title: Text("Profile"),

              onTap: () {

                mySnackBar("Profile", context);

              },

            ),

            ListTile(

              leading: Icon(Icons.mail),

              title: Text("Email"),

              onTap: () {

                mySnackBar("Email", context);

              },

            ),

            ListTile(

              leading: Icon(Icons.phone),

              title: Text("Phone"),

              onTap: () {

                mySnackBar("Phone", context);

              },

            ),

          ],

        ),

      ),

    );

  }

}
```

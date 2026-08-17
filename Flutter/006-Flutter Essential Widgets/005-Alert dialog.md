# Alert Dialog

```dart
class HomeActivity extends StatelessWidget {

  const HomeActivity({super.key});

  void mySnackBar(String message, BuildContext context) {
    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(backgroundColor: Colors.green, content: Text(message)),
    );
  }



  Future<dynamic> myAlertDialog(BuildContext context) {

    return showDialog(
      context: context,
      builder: (BuildContext context) {

        return Expanded(
          child: AlertDialog(
            title: Text("Alert!"),
            content: Text("Do you want to delete"),
           
            actions: [
              TextButton(
                onPressed: () {
                  mySnackBar("Delete success", context);
                  Navigator.of(context).pop();
                },
                child: Text("Yes"),
              ),
              TextButton(
                onPressed: () {
                  Navigator.of(context).pop();
                },
                child: Text("No"),
              ),
            ],
          ),
        );
      },
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

      ),



      body: Center(
        child: ElevatedButton(
          onPressed: () {
            myAlertDialog(context);
          },
          child: Text("Click me"),
        ),

      ),
  ),
}
```

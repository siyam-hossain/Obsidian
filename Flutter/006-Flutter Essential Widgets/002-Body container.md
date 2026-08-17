# Body container in flutter

**Container** class in clutter is a convenience widget that combines common painting, positioning, and sizing of widgets.

| ![image](https://raw.githubusercontent.com/siyam-hossain/images/refs/heads/main/Flutter/006-Flutter%20Essential%20Widgets/002-Body%20container.png) |
| --------------------------------------------------------------------------------------------------------------------------------------------------- |

```dart
body: Container(

        height: 250,

        width: 250,

        decoration: BoxDecoration(

          color: Colors.green,

          border: Border.all(color: Colors.black, width: 6),

          borderRadius: BorderRadius.all(Radius.circular(50)),

        ),

        margin: EdgeInsets.all(30),

        // padding: EdgeInsets.all(60),



        alignment: Alignment.topCenter,



        child: ClipRRect(

          borderRadius: BorderRadius.circular(44),

          child: Image.network(

            "https://avatars.githubusercontent.com/u/101579405?v=4",

            fit: BoxFit.cover,

            width: double.infinity,

            height: double.infinity,

          ),

        ),

      ),
```

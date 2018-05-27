# Flushbar

This is a flutter widget inspired by [Flashbar](https://github.com/aritraroy/Flashbar). Use this package if you need
more customization when notifying your user. For Android developers, it is made to substitute
toasts and snackbars.
Development of Flushbar and [Flashbar](https://github.com/aritraroy/Flashbar) are totally separate.
Although they look like each other, they work very differently. See the examples bellow.

## Getting Started

Since Flushbar is an offscreen widget, I made it to be wrapped 
in a [Stack](https://docs.flutter.io/flutter/widgets/Stack-class.html).
Make sure Flushbar is the last child in the Stack.

### A basic Flushbar

The most basic Flushbar needs should receive title and a message. You can set your text and title latter
if you don't have them on construction time. Simply use `changeTitle()` or `changeMessage()` or `changeTitleText()`
and `changeMessageText()`
* Keep a reference to you flushbar. You are going to need it latter for customization.

```dart
class YourAwesomeApp extends StatelessWidget {

  Flushbar flushbar = new Flushbar(
    "Hey Ninja", //title
    "Lorem Ipsum is simply dummy text of the printing and typesetting industry.", //message
  );

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'YourAwesomeApp',
      home: new Scaffold(
        body: Stack(
          children: <Widget>[YourMainScreenWidget(), flushbar],
        ),
      ),
    );
  }
}
```
![Basic Example](https://github.com/AndreHaueisen/flushbar/blob/master/readme_resources/basic_bar.png)

### Lets get crazy Flushbar

Here is how customized things can get.

```dart
Flushbar flushbar = new Flushbar(
    "Hey Ninja", //title
    "Lorem Ipsum is simply dummy text of the printing and typesetting industry",
    flushbarPosition: FlushbarPosition.TOP, //Immutable
    reverseAnimationCurve: Curves.decelerate, //Immutable
    forwardAnimationCurve: Curves.elasticOut, //Immutable
    backgroundColor: Colors.red,
    shadowColor: Colors.blue[800],
    backgroundGradient: new LinearGradient(colors: [Colors.blueGrey, Colors.black]),
    isDismissible: false,
    duration: Duration(seconds: 4),
    icon: Icon(
      Icons.check,
      color: Colors.greenAccent,
    ),
    mainButton: FlatButton(
      onPressed: () {},
      child: Text("CLAP", style: TextStyle(color: Colors.amber),),
    ),
    linearProgressIndicator: LinearProgressIndicator(backgroundColor: Colors.blueGrey,),
    titleText: new Text(
      "Hello Hero",
      style: TextStyle(
          fontWeight: FontWeight.bold,
          fontSize: 20.0,
          color: Colors.yellow[600],
          fontFamily: "ShadowsIntoLightTwo"),
    ),
    messageText: new Text(
      "You killed that giant monster in the city. Congratulations!",
      style: TextStyle(
        fontSize: 18.0,
          color: Colors.green[300],
          fontFamily: "ShadowsIntoLightTwo"),
    ),
  );
```

* Note that every property has a change...() function so you don't have to create a new Flushbar every single time. The
exceptions are `flushbarPosition`, `reverseAnimationCurve`, `forwardAnimationCurve`.
* Don't forget to call `commitChanges()` or the changes won't take effect.
* To deactivate any of those properties, pass `null` to it, with the exception of `changeTitle(title)` and `changeMessage(message)`

```dart
flushbar
    .changeTitle(title) //string
    .changeMessage(message) //string
    .changeTitleText(titleText) //Text widget
    .changeMessageText(messageText) //Text widget
    .changeDuration(duration) //Duration
    .changeIcon(icon) //Icon widget
    .changeMainButton(mainButton) //FlatButton widget
    .changeBackgroundColor(backgroundColor) //Color
    .changeBackgroundGradient(backgroundGradient) //Gradient
    .changeIsDismissible(isDismissible) //bool
    .changeShadowColor(shadowColor) //Color
    .changeLinearProgressIndicator(linearProgressIndicator) //LinearProgressIndicator widget
    .setStatusListener(onStatusChanged) //(FlashbarStatus) {}
    .commitChanges();
```

![Complete Example](https://github.com/AndreHaueisen/flushbar/blob/master/readme_resources/complete_bar.png)

### Customize your text

If you need a more fancy text, you can create a [Text](https://docs.flutter.io/flutter/widgets/Text-class.html)
and pass it to the `titleText` or `messageText` variables.
* Note that `title` will be ignored if `titleText` is used
* Note that `message` will be ignored if `messageText` is used

```dart
Flushbar flushbar = new Flushbar(
    "Hey Ninja", //title
    "Lorem Ipsum is simply dummy text of the printing and typesetting industry", //message
    titleText: new Text(
      "Hello Hero",
      style: TextStyle(
          fontWeight: FontWeight.bold,
          fontSize: 20.0,
          color: Colors.yellow[600],
          fontFamily: "ShadowsIntoLightTwo"),
    ),
    messageText: new Text(
      "You killed that giant monster in the city. Congratulations!",
      style: TextStyle(
        fontSize: 16.0,
          color: Colors.green[600],
          fontFamily: "ShadowsIntoLightTwo"),
    ),
  );
```

![Customized Text](https://github.com/AndreHaueisen/flushbar/blob/master/readme_resources/text_bar.png)

### Customize background and shadow

You can paint the background with any color you want. The same goes for shadows.
`shadow` won't show by default. You will only see a shadow if you specify a color.

```dart
Flushbar flushbar = new Flushbar(
    "Hey Ninja", //title
    "Lorem Ipsum is simply dummy text of the printing and typesetting industry",
    backgroundColor: Colors.red,
    shadowColor: Colors.red[800],
  );
```

![Background and Shadow](https://github.com/AndreHaueisen/flushbar/blob/master/readme_resources/background_color_bar.png)

Want a gradient in the background? No problem.
* Note that `backgroundColor` will be ignored while `backgroundGradient` is not null

```dart
Flushbar flushbar = new Flushbar(
  "Hey Ninja", //title
  "Lorem Ipsum is simply dummy text of the printing and typesetting industry",
  backgroundGradient: new LinearGradient(colors: [Colors.blue, Colors.teal]),
  backgroundColor: Colors.red,
  shadowColor: Colors.blue[800],
  );
```

![Background Gradient](https://github.com/AndreHaueisen/flushbar/blob/master/readme_resources/gradient_bar.png)

### Icon and button action

Lets put a Icon that has a `PulseAnimation`. Icons have this animation by default
and cannot be changed as of this moment.
* You can use `changeMainButton()` and `changeIcon()` once you have an instance.

```dart
Flushbar flushbar = new Flushbar(
  "Hey Ninja", //title
  "Lorem Ipsum is simply dummy text of the printing and typesetting industry",
  icon: Icon(
    Icons.info_outline,
    color: Colors.blue,
  ),
  mainButton: FlatButton(
    onPressed: () {},
    child: Text("ADD", style: TextStyle(color: Colors.amber),),
  ),
);
```

![Icon and Button](https://github.com/AndreHaueisen/flushbar/blob/master/readme_resources/icon_and_button_bar.png)

### Flushbar position

Flushbar can be at `FlushbarPosition.BOTTOM` or `FlushbarPosition.TOP`.
* This variable is immutable and can not be changed after the bar is created.

```dart
Flushbar flushbar = new Flushbar(
  "Hey Ninja", //title
  "Lorem Ipsum is simply dummy text of the printing and typesetting industry",
  flushbarPosition: FlushbarPosition.TOP,
);
```

![Bar position](https://github.com/AndreHaueisen/flushbar/blob/master/readme_resources/position_bar.png)

### Duration and dismiss policy

By default, Flushbar is infinite. To set a duration, use `duration` or `changeDuration()`.
By default, Flushbar is dismissible by the user. A right or left scroll will dismiss it.
Use `isDismissible` or `changeIsDismissible()` to change it.

```dart
Flushbar flushbar = new Flushbar(
  "Hey Ninja", //title
  "Lorem Ipsum is simply dummy text of the printing and typesetting industry",
  duration: Duration(seconds: 3),
  isDismissible: false,
);
```

//TODO add gif

### Progress Indicator

If you are loading something, use a [LinearProgressIndicator](https://docs.flutter.io/flutter/material/LinearProgressIndicator-class.html)

```dart
Flushbar flushbar = new Flushbar(
  "Hey Ninja", //title
  "Lorem Ipsum is simply dummy text of the printing and typesetting industry",
  linearProgressIndicator: new LinearProgressIndicator(backgroundColor: Colors.grey[800],),
);
```

//TODO add gif

### Show and dismiss animation curves

You can set custom animation curves using `forwardAnimationCurve` and `reverseAnimationCurve`.
* These properties are immutable

```dart
Flushbar flushbar = new Flushbar(
  "Hey Ninja", //title
  "Lorem Ipsum is simply dummy text of the printing and typesetting industry",
  forwardAnimationCurve: Curves.decelerate,
  reverseAnimationCurve: Curves.easeOut,
);
```

//TODO add gif

### Listen to status updates

You can listen to status update using `setStatusListener()`. 
* Note that when you pass a new listener using `setStatusListener()`, it will activate once immediately
so you can check in what state the Flushbar is.

```dart

Flushbar flushbar = new Flushbar(
  "Hey Ninja", //title
  "Lorem Ipsum is simply dummy text of the printing and typesetting industry");

flushbar.setStatusListener(
  (FlushbarStatus status){
   if(status == FlushbarStatus.DISMISSED){
     doSomething();
   }
  }
 );
```

## Usage Sample

Since you are probably going to control your Flushbar from `FirstScreen()`, pass `flushbar` as an argument.
Flushbar is an offscreen widget. It was made to be wrapped in a [Stack](https://docs.flutter.io/flutter/widgets/Stack-class.html).
Make sure Flushbar is the last child in the Stack.

```dart
class YourAwesomeApp extends StatelessWidget {

  Flushbar flushbar = new Flushbar(
    "Hey Ninja", //title
    "Lorem Ipsum is simply dummy text of the printing and typesetting industry.", //message
  );

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'YourAwesomeApp',
      home: new Scaffold(
        body: Stack(
          children: <Widget>[FirstScreen(flushbar), flushbar],
        ),
      ),
    );
  }
}
```

For consistency, create a helper class so you can mutate you Flushbar. Customize it to your need.
* Remember to pass `null` to deactivate a widget.

```dart

class FlushbarHelper {
  static Flushbar changeToInfoFlushbar(Flushbar flushbar,
      {@required String title, @required String message}) {
    return flushbar
        .changeTitle(title)
        .changeMessage(message)
        .changeIcon(
          Icon(
            Icons.info_outline,
            color: Colors.blue,
          ),
        )
        .changeDuration(Duration(seconds: 2))
        .changeMainButton(null)
        .changeLinearProgressIndicator(null);
  }

  static Flushbar changeToActionFlushbar(Flushbar flushbar,
      {@required String title,
      @required String message,
      @required FlatButton button}) {
    return flushbar
        .changeTitle(title)
        .changeMessage(message)
        .changeIcon(null)
        .changeDuration(Duration(seconds: 2))
        .changeMainButton(button)
        .changeLinearProgressIndicator(null);
  }

  static Flushbar changeToLoadingFlushbar(Flushbar flushbar,
      {@required String title,
      @required String message,
      @required LinearProgressIndicator linearProgressIndicator}) {
    return flushbar
        .changeTitle(title)
        .changeMessage(message)
        .changeIcon(
          Icon(
            Icons.cloud_upload,
            color: Colors.blue,
          ),
        )
        .changeDuration(Duration(seconds: 2))
        .changeMainButton(null)
        .changeLinearProgressIndicator(linearProgressIndicator);
  }

  static Flushbar changeToErrorFlushbar(Flushbar flushbar,
      {@required String title, @required String message}) {
    return flushbar
        .changeTitle(title)
        .changeMessage(message)
        .changeIcon(
          Icon(
            Icons.error,
            color: Colors.red,
          ),
        )
        .changeDuration(Duration(seconds: 2))
        .changeMainButton(null)
        .changeLinearProgressIndicator(null);
  }

  static Flushbar changeToConfirmFlushbar(Flushbar flushbar,
      {@required String title, @required String message}) {
    return flushbar
        .changeTitle(title)
        .changeMessage(message)
        .changeIcon(
          Icon(
            Icons.check,
            color: Colors.green,
          ),
        )
        .changeDuration(Duration(seconds: 2))
        .changeMainButton(null)
        .changeLinearProgressIndicator(null);
  }
}
```

Inside you MainScreenWidget use the reference to control it. Don't forget to `commitChanges()`

```dart
class FirstScreen extends StatelessWidget {
  FirstScreen(this.flushbar);

  final Flushbar flushbar;

  @override
  Widget build(BuildContext context) {
    return new Container(
      child: new Center(
        child: new FloatingActionButton(
          backgroundColor: Theme.of(context).accentColor,
          child: Icon(Icons.info_outline),
          onPressed: () {
            FlushbarHelper
                .changeToInfoFlushbar(flushbar,
                    title: "No connection",
                    message: "Your app is diconnected. Action not saved")
                .commitChanges();
            flushbar.show();
          },
        ),
      ),
    );
  }
}
```
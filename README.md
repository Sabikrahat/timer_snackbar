<!-- 
This README describes the package. If you publish this package to pub.dev,
this README's contents appear on the landing page for your package.

For information about how to write a good package README, see the guide for
[writing package pages](https://dart.dev/guides/libraries/writing-package-pages). 

For general information about developing packages, see the Dart guide for
[creating packages](https://dart.dev/guides/libraries/create-library-packages)
and the Flutter guide for
[developing packages and plugins](https://flutter.dev/developing-packages). 
-->

<!-- TODO: Put a short description of the package here that helps potential users
know whether this package might be useful for them.

## Features

TODO: List what your package can do. Maybe include images, gifs, or videos.

## Getting started

TODO: List prerequisites and provide or point to information on how to
start using the package.

## Usage

TODO: Include short and useful examples for package users. Add longer examples
to `/example` folder. 

```dart
const like = 'sample';
```

## Additional information

TODO: Tell users more about the package: where to find more information, how to 
contribute to the package, how to file issues, what response they can expect 
from the package authors, and more. -->

# Timer Snackbar

Timer Snackbar package let you to add a beautiful live timer at snackbar to your Flutter app.

## Installation

1. Add the latest version of package to your pubspec.yaml (and run`dart pub get`):
```yaml
dependencies:
  timer_snackbar2:
    git:
      url: https://github.com/aa2013/timer_snackbar2.git
      ref: master 
```
2. Import the package and use it in your Flutter App.
```dart
import 'package:timer_snackbar/timer_snackbar.dart';
```

## Preview

![Preview](https://raw.githubusercontent.com/aa2013/timer_snackbar2/master/sample.gif)

<br>

## Example
There are a number of properties that you can modify:

- context
- scaffoldMessengerState
- contentText
- buttonPrefixWidget
- buttonLabel
- afterExecuteMethod
- second
- backgroundColor
- contentTextStyle

<hr>

```dart
import 'package:flutter/material.dart';
import 'package:timer_snackbar/timer_snackbar.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Timer Snackbar',
        theme: ThemeData(
          primarySwatch: Colors.blue,
        ),
        home: const HomePage());
  }
}

class HomePage extends StatelessWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Row(
      children: [
        Expanded(
          child: NestedScaffold(
            title: "NestedScaffold1",
          ),
        ),
        Expanded(
          child: NestedScaffold(
            title: "NestedScaffold2",
          ),
        ),
        Expanded(
          child: MyScaffold(
            title: "MyScaffold1",
          ),
        ),
        Expanded(
          child: MyScaffold(
            title: "MyScaffold2",
          ),
        ),
      ],
    );
  }
}

class NestedScaffold extends StatelessWidget {
  final String title;

  NestedScaffold({Key? key, required this.title}) : super(key: key);
  //Use ScaffoldMessenger with a key, and pass the state when calling timerSnackbar.
  final scaffoldMessengerKey = GlobalKey<ScaffoldMessengerState>();

  @override
  Widget build(BuildContext context) {
    return ScaffoldMessenger(
      //Pay attention here
      key: scaffoldMessengerKey,
      child: Scaffold(
        appBar: AppBar(
          title: Text(title),
        ),
        body: Center(
          child: ElevatedButton(
            child: const Padding(
                padding: EdgeInsets.all(8.0),
                child: Text('Show separated snackbar', textScaleFactor: 1.2)),
            style: ElevatedButton.styleFrom(
                shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(8.0))),
            onPressed: () => timerSnackbar(
              scaffoldMessengerState: scaffoldMessengerKey.currentState!,
              contentText: "A snackbar with live timer.",
              buttonPrefixWidget: Image.asset(
                'assets/undo.png',
                width: 17.0,
                height: 15.0,
                alignment: Alignment.topCenter,
                color: Colors.blue[100],
              ),
              afterTimeExecute: () => print("Operation Execute."),
              second: 5,
            ),
          ),
        ),
      ),
    );
  }
}

class MyScaffold extends StatelessWidget {
  final String title;

  const MyScaffold({Key? key, required this.title}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: Center(
        child: ElevatedButton(
          child: const Padding(
              padding: EdgeInsets.all(8.0),
              child: Text('Show Snackbar Both', textScaleFactor: 1.2)),
          style: ElevatedButton.styleFrom(
              shape: RoundedRectangleBorder(
                  borderRadius: BorderRadius.circular(8.0))),
          onPressed: () => timerSnackbar(
            context: context,
            contentText: "A snackbar with live timer.",
            buttonPrefixWidget: Image.asset(
              'assets/undo.png',
              width: 17.0,
              height: 15.0,
              alignment: Alignment.topCenter,
              color: Colors.blue[100],
            ),
            afterTimeExecute: () => print("Operation Execute."),
            second: 5,
          ),
        ),
      ),
    );
  }
}

```



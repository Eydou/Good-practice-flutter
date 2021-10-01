**Good practice flutter**

1.  ``Performance tips``

    <span style="color:red">wrong practice</span>

    ```dart int mark = 10;
    int total = 10;
    int amount = 10;
    ```
    <span style="color:green">good practice</span>
    ```dart 
    int mark =10,
    total = 20,
    amount = 30;
    ````
2.  ``Performance tips``

    <span style="color:red">wrong practice</span>
    ```dart
    var name = "Hello World";
  
    assert(!(name is int));
    ```
    <span style="color:green">good practice</span>
    ```dart
    var name = "Hello World";
  
    assert(name is String); 
    assert(name is! int); 
    ```
3. ``Debug``

    Print slowing your app in production environment

    <span style="color:red">wrong practice</span>
    ```dart
    print('movieTitle: $movieTitle');
    ```
    <span style="color:green">good practice</span>
    ```dart
    Widget :

    import 'package:flutter/foundation.dart';
    debugPrint('movieTitle: $movieTitle');

    Otherwise :

    import 'dart:developer';
    log('data: $data');
    ```

4. ``Flutter upgrade``

    If you want to be sure that your app fully benefits from the changes introduced in the latest Flutter release, make sure you also delete and recreate the platform folder for the platform you are testing your app on: 

    <span style="color:red">wrong practice</span>
    ```dart
    flutter upgrade
    ```
    <span style="color:green">good practice</span>
    ```dart
    flutter upgrade
    rmdir /s windows
    flutter create --platforms=windows
    ```

5. ``Detect host platform``

    mobile
    ```dart
    import 'dart:io' show Platform;

    if (Platform.isAndroid) {
        // Android specific code
    } else if (Platform.isIOS) {
        // IOS specific code
    }
    ```
    for web
    ```dart
    import 'package:flutter/foundation.dart' show kIsweb;

    if (kIsweb) {
        // running on the web
    }
    ```

6. ``Use const where possible``

    If it’s already defined you can save RAM using the same widget

    <span style="color:red">wrong practice</span>
    ```dart
    x = Container();
    y = Container();
    x == y // false
    ```
    <span style="color:green">good practice</span>
    ```dart
    x = const Container();
    y = const Container();
    x == y // true
    ```
7. ``Avoid using Opacity with AnimatedBuilder``

    Changing opacity is a quite expensive animation, Flutter gives us better solutions for that

    <span style="color:red">wrong practice</span>
    ```dart
    AnimatedBuilder(
    animation: _controller,
    builder: (_, child) {
        return Opacity(
        opacity: _controller.value,
        child: child,
        );
    },
    child: Placeholder(), 
    ),
    ```
    <span style="color:green">good practice</span>
    ```dart
    FadeTransition(
    opacity: _controller,
    child: Placeholder(),
    ),

    // OR ALTERNATIVELY

    AnimatedOpacity(
   opacity: opacity,
   duration: duration,
   child: Placeholder(),
    ),
    ```
8. ``Use const where possible``

    ListView couldn’t kill its the children are not being visible to the screen. It causes consume a lot of memory if children have high-resolution images.
    By doing these options false, could lead to use of more GPU and CPU work, but it could solve our memory issue and you will get a very performant view without noticeable issues.

    <span style="color:green">good practice</span>
    ```dart
    ListView.builder(
        ...
        addAutomaticKeepAlives: false (true by default)
        addRepaintBoundaries: false (true by default)
    );
    ```

9. ``Performance tips``

    Use cascade

    <span style="color:red">wrong practice</span>
    ```dart
    main(){
    Cat cat = Cat();

    cat.color = "grey";
    cat.age=5;
    cat.meaow();
    }
    ```
    <span style="color:green">good practice</span>
    ```dart
    main(){
    Cat cat = Cat();

    Cat()
    ..color = "grey"
    ..age=5
    ..meaow();
    }
    ```
10. ``Performance tips``

    User Relative Imports

    <span style="color:red">wrong practice</span>
    ```dart
    import 'package:demo/src/utilis/firebase_utilis.dart';
    ```
    <span style="color:green">good practice</span>
    ```dart
    import '../../../utilis/firebase_utilis.dart';
    ```

11. `Avoid Using the ‘as’ Operator`

    Generally, the ‘as’ operator throws an exception if the cast is not possible, to avoid that you can use the ‘is’ operator.

    <span style="color:red">wrong practice</span>
    ```dart
    (item as Vehichle).name = 'BMW';
    ```
    <span style="color:green">good practice</span>
    ```dart
    if (item is Vehichle)
    item.name = 'BMW';
    ```
12. `Use nil instead const Container()`

    It’s just a basic Element Widget that does and costs almost nothing.
    
    source : https://pub.dev/packages/nil

    <span style="color:green">good practice</span>
    ```dart
    // good
    text != null ? Text(text) : const Container()
    // Better
    text != null ? Text(text) : const SizedBox()
    // BEST
    text != null ? Text(text) : nil
    or
    if (text != null) Text(text)
    ```
13. `Use the ‘if’ Condition Instead of Conditional Expression`

    Several times we need to render a widget based on some condition in Row and Column. If conditional expression return null in any case then we should use it if condition only.

    <span style="color:red">wrong practice</span>
    ```dart
    Widget getText(BuildContext context) {
    return Row(
    children: [
    Text(“Hi”),
    Platform.isAndroid ? Text(“MediumAndroidReader”) : null,
    Platform.isAndroid ? Text(“MediumAndroidReader”) : SizeBox(),
    Platform.isAndroid ? Text(“MediumAndroidReader”) : Container(),
    ]
    );
    ```
    <span style="color:green">good practice</span>
    ```dart
    Widget getText(BuildContext context) { 
    return Row(
    children: 
    [
    Text(“Hi”), if (Platform.isAndroid) Text(“MediumAndroidReader”) 
    ] 
    );
    }
    ```
14. `Use the ‘if’ Condition Instead of Conditional Expression`

    You should use raw strings to avoid escaping backlashes and the dollar signs.

    <span style="color:red">wrong practice</span>
    ```dart
    var text = ‘This is a demo string \\ and \$ is not raw’;
    ```
    <span style="color:green">good practice</span>
    ```dart
    var text = r'This is a demo string \\ and \$ is raw';
    ```
15. `Use Spread Collections`

    Using spread collections will simplify the code for you when the existing items are already stored in another collection.

        <span style="color:red">wrong practice</span>
        ```dart
        var a= [4,5,6];
        var b= [1,2];
        a.addAll(b);
        ```
        <span style="color:green">good practice</span>
        ```dart
        var a= [4,5,6];
        var b= [1,2,...y];
        ```
16. `Don’t Initialize Variables as Null`

    Variables in Dart are automatically initialized to null when its values is not defined so you don’t need to do that.

    <span style="color:red">wrong practice</span>
    ```dart
    int maxPage = null;
    ```
    <span style="color:green">good practice</span>
    ```dart
    int maxPage;
    ```

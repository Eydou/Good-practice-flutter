**Good practice flutter**

1.  ``Tips``

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
2.  ``Tips``

    <span style="color:red">wrong practice</span>
    ```dart
    var name = "Hello World";
  
    assert(!(name is int));
    ```
    <span style="color:green">good practice</span>
    ```dart
    var name = "Hello World";
  
    assert(name is String); 
    assert( name is! int); 
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

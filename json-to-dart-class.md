# Json To Dart Class

### Json
```json
{
    "id": "1001",
    "name": "Vipin",
    "age": 25,
    "places": [
        "India",
        "US"
    ],
    "images": [
        {
            "id": 10,
            "name": "img1"
        },
        {
            "id": 11,
            "name": "img2"
        }
    ],
    "address": {
        "street_no": "1212",
        "details": {
            "house_no": 3355,
            "town": "Test Town"
        }
    }
}
```
## Dart Class
```dart
class Person {
  final String id;
  final String name;
  final int age;
  final List<String> places;
  final List<Images> images;
  final Address address;
  Person({
    this.id,
    this.name,
    this.age,
    this.places,
    this.images,
    this.address,
  });

  factory Person.fromJson(Map<String, dynamic> json) {
    return Person(
      id: json['id'],
      name: json['name'],
      age: json['age'],
      places: personPlaces(json['places']),
      images: perseImages(json),
      address: Address.fromjson(json['address']),
    );
  }
  static List<String> personPlaces(placesJson) {
    List<String> placesList = List<String>.from(placesJson);
    return placesList;
  }

  static List<Images> perseImages(imageJson) {
    var list = imageJson['images'] as List;
    List<Images> imageList = list.map((e) => Images.fromJson(e)).toList();
    return imageList;
  }
}

class Images {
  int id;
  String name;
  Images({this.id, this.name});
  factory Images.fromJson(Map<String, dynamic> json) {
    return Images(
      id: json['id'],
      name: json['name'],
    );
  }
}

class Details {
  int houseno;
  String town;
  Details({this.houseno, this.town});

  factory Details.fromjson(Map<String, dynamic> json) {
    return Details(
      houseno: json['house_no'] as int,
      town: json['town'],
    );
  }
}

class Address {
  final String streetNo;
  final Details details;
  Address({this.streetNo, this.details});
  factory Address.fromjson(Map<String, dynamic> json) {
    return Address(
      streetNo: json['street_no'] as String,
      details: Details.fromjson(json['details']),
    );
  }
}

```
## main.dart
```dart
import 'dart:convert';

import 'package:appmy/model.dart';
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

main() => runApp(MyApp());

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  Future<String> loadPersonFromAssets() async {
    return await rootBundle.loadString('json/person.json');
  }

  Future loadPerson() async {
    String jsonString = await loadPersonFromAssets();
    final jsonResponse = json.decode(jsonString);
    Person person = Person.fromJson(jsonResponse);
    // print("name ${person.name}");
    // print("Places ${person.places}");
    // print("images ${person.images[0].name}");
    print("address ${person.address.streetNo}");
  }

  @override
  void initState() {
    super.initState();
    loadPerson();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text("CodeWithRafiq"),
        ),
        body: Center(
          child: Text(
            "Hello World",
            style: TextStyle(
              fontSize: 28,
            ),
          ),
        ),
      ),
    );
  }
}

```

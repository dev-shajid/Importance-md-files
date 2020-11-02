
## Java, Computer License
> android\key.properties
<p> 
  storePassword=1234@1234 <br />
  keyPassword=1234@1234<br />
  keyAlias=key<br />
  storeFile=../../key.jks
</p>

## InterNet connection on APP
> android\app\src\main\AndroidManifest.xml

`<uses-permission android:name="android.permission.INTERNET"/>`

## splash screens
> android\app\src\main\res\drawable\launch_background.xml

```bash
<item>
  <color android:color="@color/splash" />  
</item>
<item>
  <bitmap
  android:gravity="center"
  android:src="@drawable/icon" />
</item>
```

## splash Color

> android\app\src\main\res\values\colors.xml

`<resources>
<color name="ic_launcher_background">#008EFF</color>
<color name="splash">#008EFF</color>
</resources>`

## Internet Connaction in App
> android\app\src\debug\AndroidManifest.xml
```bash
<uses-permission android:name="android.permission.INTERNET"/>
```
## Icon Color
```
dev_dependencies:
  flutter_launcher_icons: ^0.8.1
flutter_icons:
  android: true
  ios: true
  image_path: "assets/icon.png"
  adaptive_icon_background: '#008EFF'
  adaptive_icon_foreground: "assets/icon.png"
```
## Splish Screens
> android\app\src\main\res\drawable-hdpi\icon.png
## GO TO THIS WEBPAGE
### [Build and release an Android app](https://flutter.dev/docs/deployment/android)

##  Change App Name 
>`
android\app\src\main\AndroidManifest.xml =>android:label="<app name>"
`
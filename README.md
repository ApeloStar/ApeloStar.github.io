## Getting Started  
</br>

#### 1. Update dependencies
```
flutter pub get
```

#### 2. Run following command to create build folders
```
flutter create --org com.bpc.crossplatform .
```

#### 3. To generate JSON serialization and deserialization annotations used by json_serializable run:
```
flutter packages pub run build_runner build
```
if it pass error, try the same command with key `--delete-conflicting-outputs`

#### 4. Set the app icon
```
flutter pub run flutter_launcher_icons:main
```

</br>

## iOS setup

1. Uncomment ```platform :ios, '9.0'``` in `/ios/Podfile`

2. Add these lines into your `/ios/Runner/info.plist`
```
<key>NSCameraUsageDescription</key>
<string>This app needs camera access to scan cards and QR codes</string>
<key>NSMicrophoneUsageDescription</key>
<string>This application needs to access your microphone to recognize speech</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>This application needs to access your gallery</string>
<key>NSSpeechRecognitionUsageDescription</key>
<string>This application needs the speech recognition permission</string>
<key>io.flutter.embedded_views_preview</key>
<true/>
```
3. Next step, to allow GoogleMaps work, open `ios/Runner/AppDelegate.swift` and provide GMSServices ApiKey
```
import UIKit
import Flutter
import GoogleMaps

@UIApplicationMain
@objc class AppDelegate: FlutterAppDelegate {
  override func application(
    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
    GMSServices.provideAPIKey("YOUR KEY HERE")
    GeneratedPluginRegistrant.register(with: self)
    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }
}
```
<details>
<summary>Objective-C</summary>

```
#include "AppDelegate.h"
#include "GeneratedPluginRegistrant.h"
#import "GoogleMaps/GoogleMaps.h"

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [GMSServices provideAPIKey:@"YOUR KEY HERE"];
  [GeneratedPluginRegistrant registerWithRegistry:self];
  return [super application:application didFinishLaunchingWithOptions:launchOptions];
}
@end
```
</details>
<br>

if you want to debug the app on a real iOS device, you will need to sign the app with Apple developer account signification. If you have it, open `/ios/Runner.xcworkspace`, select project `Runner`, then go into `Signing & Capabilities`. Select `Team` and set check near the `Automatically manage signing`.

</br>

## Android setup

Firstly, change minSdk version to `24` in your `/android/app/build.gradle`

Then add these lines into your `/android/app/src/main/AndroidManifest.xml`
```
<manifest ...
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.CAMERA" />
    ...
    <application ...
        <meta-data 
            android:name="com.google.android.geo.API_KEY"
            android:value="YOUR KEY HERE"
          />
```


Then add google-services.json into your `/android/app/`





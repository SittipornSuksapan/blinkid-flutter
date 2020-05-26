# BlinkID SDK Flutter

This repository contains Flutter wrappers for BlinkID native SDKs ([iOS](https://github.com/BlinkID/blinkid-ios)
and [Android](https://github.com/BlinkID/blinkid-android)). Not all features of native SDKs are available. However, the wrapper is open source so you can add features that you need. For 100% of features and maximum control, consider using native SDKs.

## Requirements
BlinkID plugin is developed with Flutter SDK version 1.17.11.
For help with Flutter, view official [documentation](https://flutter.dev/docs).

## Getting Started
To get started, first clone the repository:
```shell
git clone https://github.com/BlinkID/blinkid-flutter.git
```

### Quick start with sample app
To try BlinkID plugin, there is a minimal sample application in the `blinkid_flutter_sample` folder.
Sample currently works only on iOS devices.

To run sample application, use the following commands:
```shell
cd blinkid_flutter_sample/
flutter run
```
If there are problems with running the application, please make sure you have
properly configured tools by running `flutter doctor`. You can also try running
the application from VSCode or Xcode.

### Plugin integration
1. Integrate BlinkId plugin in your application by setting path to the cloned repository
in your `pubspec.yaml`:
```yaml
dependencies:
  ...
  blinkid_flutter:
    path: path/to/blinkid-plugin
```

2. Perform scanning by calling the method `BlinkIDFlutter.scanWithCamera()` and passing it the `RecognizerCollection` and `OverlaySettings` you wish to use, along with your license key. To find out more about licensing, click
 [here](#licensing).
```
Future<void> scan() async {
    List<RecognizerResult> results;
    
    Recognizer recognizer = BlinkIdCombinedRecognizer();
    OverlaySettings settings = BlinkIdOverlaySettings();

    // set your license
    if (Theme.of(context).platform == TargetPlatform.iOS) {
      license = "";
    } else if (Theme.of(context).platform == TargetPlatform.android) {
      license = "";
    }

    try {
      // perform scan and gather results
      results = await BlinkIDFlutter.scanWithCamera(RecognizerCollection([recognizer]), settings, license);

    } on PlatformException {
      // handle exception
    }
```

3. When scanning is completed, variable `results` will contain a list of non-empty RecognizerResults from recognizers set in `RecognizerCollection`. You can then access each result individually. If the scanning is manually closed, the method will return an empty list.

For more information please refer to our sample application source code.

### Available API
All available recognizers can be found inside `blinkid_flutter/lib/recognizers`.

All available recognizers can be found inside `blinkid_flutter/lib/overlays`.

For 100% of features and maximum control, consider using native SDK.

### Platform specifics
Plugin implementation is in folder `lib`, while platform specific implementations are in `android` and `ios` folders.

#### Android
\#TBD

#### iOS
To initialize BlinkID framework for use with iOS, after you've added the dependency to `blinkid_flutter` to your pubspec.yaml, go to `NameOfYourProject/ios`and run `pod install`.
Our blinkid_flutter depends on the latest PPBlinkID pod so it will be installed automatically.

To set camera permission usage message, open `NameOfYourProject/ios/Runner.xcworkspace` and under Runner/Runner/Info.plist set 
`Privacy - Camera Usage Description`.

## Licensing
- [Generate](https://microblink.com/login?url=/customer/generatedemolicence) a **free demo license key** to start using the SDK in your app (registration required)
- Get information about pricing and licensing of [BlinkID](https://microblink.com/blinkid)

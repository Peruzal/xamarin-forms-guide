description: Xamarin.Essentials provides a single cross-platform API that works with any iOS, Android, or UWP application that can be accessed from shared code no matter how the user interface is created.

# Xamarin.Essentials Cross Platform API

Xamarin.Essentials provides a single cross-platform API that works with any iOS, Android, or UWP application that can be accessed from shared code no matter how the user interface is created.

## Setup

You will need to configure each platform specific project. First add the using statement :

```csharp
using Xamarin.Essentials;
```

### Android Configuration

In the `OnCreate` method add the following :

```csharp
Xamarin.Essentials.Platform.Init(this, bundle);
```

and to handle runtime permissions, add this also :

```csharp
public override void OnRequestPermissionsResult(int requestCode, string[] permissions, [GeneratedEnum] Android.Content.PM.Permission[] grantResults)
{
    Xamarin.Essentials.Platform.OnRequestPermissionsResult(requestCode, permissions, grantResults);

    base.OnRequestPermissionsResult(requestCode, permissions, grantResults);
}
```

### iOS Configuration

No specific configuration is required for iOS.

### Xamarin Essentials Features

Feature | Description
------- | -------
Accelerometer | Retrieve acceleration data of the device in three dimensional space.
App Information | Find out information about the application.
Battery | Easily detect battery level, source, and state
Clipboard | Quickly and easily set or read text on the clipboard.
Compass | Monitor compass for changes.
Connectivity | Check connectivity state and detect changes.
Data Transfer | Send text and website uris to other apps.
Device Display Information | Get the device's screen metrics and orientation.
Device Information | Find out about the device with ease.
Email | Easily send email messages.
File System Helpers | Easily save files to app data.
Flashlight | A simple way to turn the flashlight on/off.
Geocoding | Geocode and reverse geocode addresses and coordinates.
Geolocation | Retrieve the device's GPS location.
Gyroscope | Track rotation around the device's three primary axes.
Magnetometer | Detect device's orientation relative to Earth's magnetic field.
Open Browser | Quickly and easily open a browser to a specific website.
Orientation Sensor | Retrieve the orientation of the device in three dimensional space.
Phone Dialer | Open the phone dialer.
Platform | Run code on the application's main thread.
Preferences | Quickly and easily add persistent preferences.
Screen Lock | Keep the device screen awake.
Secure Storage | Securely store data.
SMS | Create an SMS message for sending.
Text-to-Speech | Vocalize text on the device.
Version Tracking | Track the applications version and build numbers.
Vibrate | Make the device vibrate.
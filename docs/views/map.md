# Map

Xamarin Forms will use the native map control on each platform. On Android it will use the Google Maps and on iOS the Apple Maps. The Maps needs to be configured.

## Add Nuget Package

The Maps is included as a separate Nuget package. Add the `Xamarin.Forms.Maps` nuget package to every project in the solution.

### Initialize iOS Project

Navigate to the iOS project and add `Xamarin.FormsMaps.Init();` after the `Xamarin.Forms.Init()` line in the AppDelegate.cs file :

```csharp
global::Xamarin.Forms.Forms.Init();
Xamarin.FormsMaps.Init();

LoadApplication(new App());
```

On simulator, you should be able to create a new Map as follows:

```csharp
    public partial class MapsPage : ContentPage
    {
        public MapsPage()
        {
            InitializeComponent();
            Content = new Map();
        }
    }
```

You will also need to add  get permission from the user for accessing their location. Add the following in the Info.plist file :

```xml
<key>XSAppIconAssets</key>
<string>Assets.xcassets/AppIcon.appiconset</string>
<key>NSLocationWhenInUseUsageDescription</key>
<string>App is using your location</string>
```

After adding the configs in the Info.plist file, we can now show the users location as follows :

```csharp
Content = new Map {
    IsShowingUser = true,
    MapType = MapType.Hybrid
};
```

### Configure Android

In the MainActivity.cs file add the following line `Xamarin.FormsMaps.Init(this,bundle);` after the `Xamarin.Forms.Init(this,bundle);` line. The modified file should be as follows :

```csharp
protected override void OnCreate(Bundle bundle)
{
    TabLayoutResource = Resource.Layout.Tabbar;
    ToolbarResource = Resource.Layout.Toolbar;

    base.OnCreate(bundle);

    global::Xamarin.Forms.Forms.Init(this, bundle);
    Xamarin.FormsMaps.Init(this,bundle);

    LoadApplication(new App());
}
```

#### Obtain API Key

You will need to obtain an API Key to use the Google Maps for Android. They are two keys used, one for debug and another one for production.

Following this guide on getting an API Key for Google Maps, [Obtain Google Maps API Key](https://developer.xamarin.com/guides/android/platform_features/maps_and_location/maps/obtaining_a_google_maps_api_key/)

During development you can register the debug key on the Google Console.

#### Get SHA1 Fingerprint

To get the SHA1 fingerprint for the debug key run the following on the command line

```xml
keytool -v -list -keystore ~/.local/share/Xamarin/Mono\ for\ Android/debug.keystore
```

The default password is `android`

#### Add the API Key to the AndroidManifest.xml

The Google Maps key needs to be added inside the &lt;application&gt;&lt;/application&gt; in the AndroidManifest.xml file.

```xml
<meta-data android:name="com.google.android.maps.v2.API_KEY"
            android:value="<Replace with your API Key Here>" />
```

Add Permission

You will need to add the following permissions to the AndroidManifest.xml file :

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_MOCK_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_LOCATION_EXTRA_COMMANDS" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```
description: A Switch allows toggling its value to true and false.

# Switch

A Switch allows toggling its value to true and false.

## Define in XAML

```xml
<Switch IsToggled="true" />
```

## Define in Code

```csharp
var attendingSwitch = new Switch
{
    IsToggled = true
};
```

## Change Color

The color for the Swith can be changed for each platform. 

### Android

These changes should be made in the Android project

- Open the `styles.xml` file located under `Resources` -> `values` folder
- Change the `<item name="colorAccent">#FF4081</item>` and assing your designed color

### iOS

These changes should be made in the iOS project

- Open the `AppDelegate.cs` file
- Within the method `FinishedLaunching` add the following lines

```cs
// You can also use UIColor.FromRGB to assign colors using RGB values
// Eg assign a green color UIColor.FromRGB(0x91, 0xCA, 0x47)
UISwitch.Appearance.OnTintColor = UIColor.Orange; 
```

The complete method should be as follows :

```cs
public override bool FinishedLaunching(UIApplication app, NSDictionary options)
{
    UISwitch.Appearance.OnTintColor = UIColor.Orange;
    global::Xamarin.Forms.Forms.Init();
    LoadApplication(new App());

    return base.FinishedLaunching(app, options);
}
```
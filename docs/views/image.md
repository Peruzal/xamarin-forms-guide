# Image

The control is used to display images.

## In XAML

> Note that you will need to put the image into each platform.

```xml
<Image Source="logo" />
```

The logo.png image was added to the Android drawable folder and on iOS into the Assets.xcassets folder.

## In Code

**Local image**

```csharp
var localImage = new Image
{
    Source = "logo"
};
```

**Download image from the internet**

```csharp
var image = new Image
{
    Source = new UriImageSource
    {
        Uri = new Uri("https://i.imgur.com/OM81S7f.png")
    }
};
```


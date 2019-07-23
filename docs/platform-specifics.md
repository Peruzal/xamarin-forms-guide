

## Use Safe Area

```xml
<?xml version="1.0" encoding="UTF-8"?> 
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" 
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
    xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core" 
    ios:Page.UseSafeArea="true" >
```


```csharp
using Xamarin.Forms.PlatformConfiguration.iOSSpecific;
using Xamarin.Forms;
 
namespace iPhoneX 
{
 public partial class ItemsPage : ContentPage
 {
 public ItemsPage()
 {
 InitializeComponent();
 
 On<Xamarin.Forms.PlatformConfiguration.iOS>().SetUseSafeArea(true);
 }
 }
}
```

```csharp
C#
On<Xamarin.Forms.PlatformConfiguration.iOS>().SetPrefersLargeTitles(true);
1
On<Xamarin.Forms.PlatformConfiguration.iOS>().SetPrefersLargeTitles(true);
```

```csharp
public partial class ItemsPage : ContentPage
{
    public ItemsPage()
    {
        InitializeComponent();
        On<Xamarin.Forms.PlatformConfiguration.iOS>().SetLargeTitleDisplay(LargeTitleDisplayMode.Never);
    }
    ...
}
```
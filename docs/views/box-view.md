# BoxView

The BoxView is used to draw a solid colored rectangle. Xamarin does not have the other shapes out of the box. By default the size of the BoxView is 40x40 but you can use the WidthRequest and HeightRequest property to choose different sizes.

## In XAML

```xml
<BoxView Color="Orange" HorizontalOptions="Center" VerticalOptions="Center" />
```

## In Code

```csharp
var boxView = new BoxView
{
    HorizontalOptions = LayoutOptions.Center,
    VerticalOptions = LayoutOptions.CenterAndExpand,
    WidthRequest = 100,
    HeightRequest = 100                    
};
```
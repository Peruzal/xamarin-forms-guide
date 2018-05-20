# Slider

A view control that inputs a linear value. The control looks similar to a progress bar but allows scrubbing.

## Define in XAML

```xml
<Slider Minimum="0" Maximum="100" Value="20" x:Name="slider" />
```

We could use data binding and show the value of the Slider as follows :

```xml
<StackLayout>
    <Label BindingContext="{x:Reference slider}" Text="{Binding Value, StringFormat='The value is {0:F d}'}" />
    <Slider Minimum="0" Maximum="100" Value="20" x:Name="slider" />
</StackLayout>
```

## Define in Code

```csharp
var videoSlider = new Slider
{
    Value = 5,
    Minimum = 0,
    Maximum = 10
};
```




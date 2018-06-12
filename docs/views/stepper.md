description: A Stepper allows inputting a discrete value that is constrained to a range.

# Stepper

A Stepper allows inputting a discrete value that is constrained to a range.

## Define in XAML

```xml
<Stepper Minimum="0" Maximum="10" x:Name="stepper" />
```

Lets display the value of the stepper using data binding in a label as follows :

```xml
<StackLayout x:Name="Container">
    <Label BindingContext="{x:Reference stepper}" Text="{Binding Value}" />
    <Stepper Minimum="0" Maximum="10" x:Name="stepper" Increment="0.5" />
</StackLayout>
```

## Define in Code

```csharp
var ageStepper = new Stepper
{
    Minimum = 18,
    Maximum = 65
};
```




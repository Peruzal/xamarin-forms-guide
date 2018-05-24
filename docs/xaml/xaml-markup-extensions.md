# XAML Markup Extension

The XAML markup extension adds additional functionality thats not defined in the standard XAML spec.

## x:Static

The `x:Static` extension can be used to access any one of the following from XAML: 

* a public static field
* a public static property
* a public constant field
* an enumeration member

## Referencing static fields

We can reference any static fields, whether from the .net framework or our own code. In the sample below we will reference a static field from our own class :

*MonthsPage.cs*

```csharp
namespace LayoutSample
{
    public partial class MonthsPage : ContentPage
    {
        public static string[] Months = new[]{
                "January",
                "February",
                "March",
                "April",
                "May",
                "June",
                "July",
                "August",
                "September",
                "October",
                "November",
                "December"
            };

        public MonthsPage()
        {
            InitializeComponent();
        }
    }
}
```

*MonthsPage.xaml.cs*

```csharp
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage 
    xmlns="http://xamarin.com/schemas/2014/forms" 
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
    xmlns:local="clr-namespace:LayoutSample"
    x:Class="LayoutSample.MonthsPage">
    <ContentPage.Content>
        <ListView ItemsSource="{x:Static local:MonthsPage.Months}" />
    </ContentPage.Content>
</ContentPage>
```

!!! note
    To refer to the static member, `Months` we first have to define the namespace in which the member is found. We define the namespace as follows `xmlns:local="clr-namespace:LayoutSample"`.

We can now use the `x:Static` extension to refer to the static property `Months` defined in the `MonthsPage`.


**Add a blank space to a label**

We are going to use the `Environment.NewLine` defined in the `System` class to add a newline to the contents of the label.

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage 
    xmlns="http://xamarin.com/schemas/2014/forms" 
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
    xmlns:sys="clr-namespace:System;assembly=mscorlib"
    x:Class="DataBindingDemo.SharedResources.MarkupExtensionPage">
    <ContentPage.Content>
        <Label>
            <Label.FormattedText>
                <FormattedString>
                    <Span Text="I am the first line" />
                    <Span Text="{x:Static sys:Environment.NewLine}" />
                    <Span Text="{x:Static sys:Environment.NewLine}" />
                    <Span Text="am separated by a new line" />
                </FormattedString>
            </Label.FormattedText>
        </Label>
    </ContentPage.Content>
</ContentPage>
```

We define the namespace for `System` using the `xmlns:sys="clr-namespace:System;assembly=mscorlib"`. Since the property `NewLine` is static, we can use it in the `Span` with `x:Static` extension by using `<Span Text="{x:Static sys:Environment.NewLine}" />`.

## StaticResource Markup Extension

The `StaticResource` is XAML markup extension is used to retrieve objects defined in the `ResourceDictionary`.

We can use the `ResourceDictionary` to keep arbitrary objects referenced by a key. In the following example, we define a color resource and double resource. We use the keys when defining the resources. We can then later on use the `StaticResource` to retrieve the object by the key.

```xaml
    <ContentPage.Resources>
        <ResourceDictionary>
            <Color x:Key="ColorPrimary">#ff9900</Color>
            <x:Double x:Key="BorderSize">1</x:Double>
        </ResourceDictionary>
    </ContentPage.Resources>
```

Use the color resource defined as follows :

```xaml
<Button 
    Text="Login" 
    BorderColor="{StaticResource ColorPrimary}" 
    BorderWidth="{StaticResource BorderSize}" /> 
```

## Platform Specific Keys

We can define keys that should be only be available on a specific platform using the `OnPlatform`. Since the `OnPlatform` is a generic object, we will need to specify the `x:TypeArguments`.

```xaml
<ResourceDictionary>
    <OnPlatform 
        x:Key="PaddingiOS" 
        x:TypeArguments="Thickness" 
        iOS="0,20,0,0" />
</ResourceDictionary>
```

The object will only be available on iOS, and we can use it the same way.

```xaml
<StackLayout Padding="{x:StaticResource PaddingiOS}">  
</StackLayout>
```

## Accessing the Resources in Code

We can access the objects defined in the `ResourceDictionary` by accessing them using the `Resources` property. Since its a dictionary, we can use the key to retrieve the object.

```xaml
<Application xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="DataBindingDemo.App">
    <Application.Resources>
        <ResourceDictionary>
            <Color x:Key="ColorPrimary">#CC0033</Color>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

We have defined a color in the application resources. The resources defined in the application resources will be available anywhere in the app. We can use both XAML or code to access them.

Let's retrieve the color and apply it to navigation bar :

```csharp
MainPage = new NavigationPage(new MainTabsPage())
{
    BarBackgroundColor = (Color)Resources["ColorPrimary"],
    BarTextColor = Color.White
};
```

Since we know the resource object is type color, we were bold as cast it to the `Color` class.


## `DynamicResource` XAML Markup Extension

The `DynamicResource` extension is similar to the `StaticResource` extension with one difference, it maintains a reference to the object. If the resource changes, then the updates are reflected.

If we have the following in the resource dictionary :

```xaml
<ResourceDictionary>
    <x:String x:Key="CurrentDate">Will show a date if accessed dynamically</x:String>
</ResourceDictionary>
```

and then use the `StatiResource` and `DynamicResource` to access the same key, you will notice that the one accessed using the `DynamicResource` will update since we have a timer running every second :

```xaml
<Label Text="{StaticResource CurrentDate}" />
<Label Text="{DynamicResource CurrentDate}" />
```

and in code we update the resource :

```csharp
Device.StartTimer(TimeSpan.FromSeconds(1), () =>
{
    Resources["CurrentDate"] = DateTime.Now.ToString("hh:mm:ss");
    return true;
});
```
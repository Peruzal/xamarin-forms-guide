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

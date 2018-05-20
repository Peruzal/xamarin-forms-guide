# Picker

The picker is used to select from a list of choices. The Picker visual appearance is similar to an Entry but instead of using a keyboard, you choose from a predefined list of elements.

## Define in XAML

```xml
 <Picker Title="Day" ItemsSource="{StaticResource DaysOfWeek}" />
```

The DaysOfWeek is a static resource array define in the XAML file as follows :

```xml
    <ContentPage.Resources>
        <ResourceDictionary>
            <x:Array x:Key="DaysOfWeek" Type="{x:Type x:String}">
                <x:String>Monday</x:String>
                <x:String>Tuesday</x:String>
                <x:String>Wednesday</x:String>
                <x:String>Thursday</x:String>
                <x:String>Friday</x:String>
                <x:String>Saturday</x:String>
                <x:String>Sunday</x:String>
            </x:Array>
        </ResourceDictionary>
    </ContentPage.Resources
```

We can also use a static member of the backing class as the source of the picker view as follows :

```xml
<Picker Title="Month" ItemsSource="{x:Static local:PickerPage.Months}" />
```

and in the backing code file :

```csharp
    public partial class PickerPage : ContentPage
    {
        public static string[] Months =  {
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sept",
            "Oct",
            "Nov",
            "Dec"
        };
        public PickerPage()
        {
            InitializeComponent();
        }
    }
```

Notice we are using the XAML extension x:Static to use static resources.

### Provide Picker Source in Code

We can altenatively proved the source of the Picker in code, as follows :

```xml
<Picker Title="Year" x:Name="pickerYear" />
```

And in the backing code file :

```csharp
pickerYear.ItemsSource = new List<string> {
    "2000",
    "2001",
    "2002",
    "2003",
    "2004"
};
```

## Define Picker in Code

We can also define and populate the Picker from code as follows:

```csharp
var picker = new Picker()
{
    ItemsSource = new List<string> {
        "Jan",
        "Feb",
        "Mar"
    }
};
```
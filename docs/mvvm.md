description: The pattern enforces a separation between three software layers — the XAML user interface, called the View; the underlying data, called the Model; and an intermediary between the View and the Model, called the ViewModel. The View and the ViewModel are often connected through data bindings defined in the XAML file.

# Model View ViewModel (MVVM)

The MVVM pattern enforces separation between the UI, the view, the data, model and the interaction between the model and the view, view-model. The View and the ViewModel are connected through data bindings.

## A Simple ViewModel

To demonstrate MVVM we will create a simple ViewModel to display the current time. In this instance we won't have a Model since the the app is so simple however we will create the View, UI and the ViewModel.

### Define the ViewModel

_ClockViewModel.cs_
```csharp
using System;
using System.ComponentModel;
using System.Runtime.CompilerServices;
using Xamarin.Forms;
namespace Models
{
    public class ClockViewModel : INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;
        DateTime dateTime;

        public ClockViewModel()
        {
            this.DateTime = DateTime.Now;
            Device.StartTimer(TimeSpan.FromSeconds(1), () =>
            {
                this.DateTime = DateTime.Now;
                return true;
            });
        }

        public DateTime DateTime {
            get {
                return dateTime;
            }

            set {
                if (value != dateTime)
                {
                    dateTime = value;
                    OnPropertyChanged();
                }
            }
        }

        public void OnPropertyChanged([CallerMemberName]string propertyName = null){
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
        }
    }
}
```

We implement the *INotifyPropertyChanged* interface. It contains one property *PropertyChanged* event. We call the event each time the property is set. This is the glue for the data binding.

### Define the View

We define the UI in XAML and use data binding to bind the ViewModel properties to the label. The *BindingContext* is define in a *ResourceDictionary*. Note that we could have set this up in code, but instead we decided to set it up in XAML.

*DemoView.xaml*
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" 
             xmlns:sys="clr-namespace:System;assembly=mscorlib"
             xmlns:local="clr-namespace:Models"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
             x:Class="CommonViewsApp.DataBinding.DataBindingDemoPage">
    <ContentPage.Resources>
        <ResourceDictionary>
            <local:ClockViewModel x:Key="vm" />
        </ResourceDictionary>
    </ContentPage.Resources>        
        <StackLayout>
            <Label BindingContext="{x:StaticResource vm}" Text="{Binding DateTime, StringFormat='{0:T}'}" />
        </StackLayout>
</ContentPage>
```

1. We first define the namespace with the Model using the following `xmlns:local="clr-namespace:Models"`.
2. We instantiated the `ClockViewModel` in in a `ResourceDictionary` with <local:ClockViewModel x:Key="vm" />. Notice that we defined a key `vm` that we will use later to reference the `ViewModel`.
3. We did bind the `Label` to the `ViewModel` using `BindingContext="{x:StaticResource vm}"`. and the Label's Text property to the `DateTime` property within the `ViewModel` with `Text="{Binding DateTime, StringFormat='{0:T}'}"` and also formatted the date to only get the time.
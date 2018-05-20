# Introduction XAML

![XAML](../images/xaml.png)

XAML stands for Extensible Markup Language. Its used in developing Windows UWP applications. XAML is also used to develop the user interface for Xamarin.Forms applications.

The version for Windows UWP is not the same as the one used for Xamarin.Forms applications but the there's effort to make them standard.

## Design Interface

Unfortunately there's not drag and drop interface for XAML as with Android Studio or XCode. However the intellisense in Visual Studio is very good. There's a Xamarin.Forms Previewer so you can preview before running the app.

## File Structure

XAML files are composed of two files. The UI and the code behind. If we were to create an example Login page we would have the following :

* `Login.xaml` - XAML UI
* `Login.xaml.cs` - Code behind for the UI

## Code vs XAML

Instead of using XAML, we can also create the UI entirely in code.

!!! note
    Creating UIs in code is not recommended and does not promote code sharing. When creating most apps, designers need to beautify the app, and not many designers can code. Designers can easily work in XAML without have to touch the underlying code for the app.

*Login.xaml*

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" 
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
             x:Class="TextSample.XAML.LoginPage">
    <ContentPage.Content>
    </ContentPage.Content>
</ContentPage>
```

*Login.xaml.cs*

```csharp
using System;
using System.Collections.Generic;

using Xamarin.Forms;

namespace TextSample.XAML
{
    public partial class LoginPage : ContentPage
    {
        public LoginPage()
        {
            InitializeComponent();
        }
    }
}
```

## Page Content

XAML pages derive from the `ContentPage` class. The contents of a `ContentPage` are assigned in the `Content` property. The `Content` property can only take one child. In XAML, `Content` property is the default, so we do not need to specify it, we can just start populating the content as follows :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" 
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
             Padding="20"
             Title="Login"
             x:Class="TextSample.XAML.LoginPage">

    <StackLayout Spacing="10">
        <Entry Placeholder="Username" Keyboard="Email" />
        <Entry Placeholder="Password" Keyboard="Text" IsPassword="true" />
        <Button Text="Login" BackgroundColor="Orange" TextColor="White" />
    </StackLayout>
</ContentPage>
```

With the XAML previewer we can see the preview as we build the page.

![XAML Preview](../images/xaml-preview.png)

## Referencing XAML Controls in Code

To have access to the XAML controls in code, we can use the predefined XAML namespace `xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml`. This is already defined for you when you create a new XAML page. We can use `x:Name` extension to give variable names to controls, and those variable names will be automatically be available in the code behind file.

```xml
<Button Text="Login" BackgroundColor="Orange" TextColor="White" x:Name="btnLogin" />
```

In the code behind file, we will now have a variable called `btnLogin`. We can now manipulate the variable however we want.

## Adding Events to Controls

We can also attach events directly to controls in XAML. E.g to have the attach the `TextChanged` event to the username filed defined above :

**In XAML**

```xml
<Entry Placeholder="Username" Keyboard="Email" TextChanged="UsernameChanged" />
```

**In Code**

```csharp
void UsernameChanged(object sender, Xamarin.Forms.TextChangedEventArgs e)
{
    throw new NotImplementedException();
}
```

## Complex Properties

Most of the properties set on the views are complex objects, e.g the `Margin` is of type `Thickness`. There are two ways to set the value. 

**Value Converter**
Using a value converter, we can easily set a complex property. E.g, to set the padding to 20 for the content page, we can do the following :

```xml

```

## Attached Properties

We can also have properties not defined on that control be made available by attaching them. Properties can be attached when the control is embedded inside the outer control that have the property available. E.g, the `Grid` layout, defines `Grid.Row` and `Grid.Column`. We can have these controls available to child controls of the grid e.g

![Label Grid](../images/label-grid.png)

```xml
<Grid>
  <Grid.RowDefinitions>
    <RowDefinition Height="*" />
    <RowDefinition Height="*" />
  </Grid.RowDefinitions>
  <Grid.ColumnDefinitions>
    <ColumnDefinition Width="*" />
    <ColumnDefinition Width="*" />
  </Grid.ColumnDefinitions>
  <Label Text="Top Left" Grid.Row="0" Grid.Column="0" />
  <Label Text="Top Right" Grid.Row="0" Grid.Column="1" />
  <Label Text="Bottom Left" Grid.Row="1" Grid.Column="0" />
  <Label Text="Bottom Right" Grid.Row="1" Grid.Column="1" />
</Grid>
```

The `Label` control does not have a property of type `Grid.Row`. Since the `Label` is a child of the `Grid`, we can attach the property to the `Label`.
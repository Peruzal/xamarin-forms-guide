description: The `StackLayout` is one of most commonly used layouts. It stacks its children in either horizontal or vertical orientation.

# Stack Layout

The `StackLayout` is one of most commonly used layouts. It stacks its children in either horizontal or vertical orientation. The default orientation if Vertical. Position and size of views is based on the `HeightRequest`, `WidthRequest`, `HorizontalOptions` and `VerticalOptions`.

The following is a sample login page. We have gone and embedded the **StackLayout** in a **ScrollView** as well so that the user can scroll up when the keyboard hides the text fields :

```xml
<?xml version="1.0" encoding="utf-8"?>
<ContentPage Padding="10" 
    xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core" 
    ios:Page.UseSafeArea="true"             
    xmlns="http://xamarin.com/schemas/2014/forms" 
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
    xmlns:local="clr-namespace:LayoutDemov1" 
    x:Class="LayoutDemov1.MainPage">
    <ScrollView Margin="0,20,0,0">
            <StackLayout Spacing="10">
              <Image Source="logo" WidthRequest="100" HeightRequest="100" />
              <Label Text="Peruzal Login" HorizontalOptions="Center" TextColor="Gray" />  
              <Entry Placeholder="Username" Keyboard="Email" />
              <Entry Placeholder="Password" IsPassword="true" />
              <StackLayout Orientation="Horizontal">
                    <Button Text="Login" HorizontalOptions="FillAndExpand" BackgroundColor="Orange" TextColor="White"/>
                    <Button Text="Register" HorizontalOptions="FillAndExpand" BackgroundColor="Gray" TextColor="White" />
              </StackLayout>
            <Label Text="Terms and Conditions" TextColor="Gray" HorizontalOptions="Center" VerticalOptions="EndAndExpand" />
            </StackLayout>            
    </ScrollView>
</ContentPage>
```

The demo shows the following sample screen on iOS.

![Stack layout][1]

In the above code we also embedded a StackLayout inside another `StackLayout` and changed the orientation to horizontal for the buttons.

[1]: /images/stacklayout.png
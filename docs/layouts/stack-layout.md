# Stack Layout

The StackLayout is one of most commonly used layouts. It stacks its children in either horizontal or vertical orientation. The default orientation if Vertical. Position and size of views is based on the `HeightRequest`, `WidthRequest`, `HorizontalOptions` and `VerticalOptions`.

The following is a sample login page. We have gone and embedded the **StackLayout** in a **ScrollView** as well so that the user can scroll up when the keyboard hides the text fields :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage  
    xmlns="http://xamarin.com/schemas/2014/forms" 
    xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" 
    Padding="10"
    x:Class="Demo.LoginPage">
    <ContentPage.Content>
    <ScrollView>
        <StackLayout>
            <StackLayout VerticalOptions="CenterAndExpand" Spacing="10">
              <Image Source="logo" WidthRequest="100" HeightRequest="100" />
              <Label Text="Login Here!" HorizontalOptions="Center" TextColor="Gray" />  
              <Entry Placeholder="Username" Keyboard="Email" />
              <Entry Placeholder="Password" IsPassword="true" />
              <StackLayout Orientation="Horizontal">
                    <Button Text="Login" HorizontalOptions="FillAndExpand" BackgroundColor="Orange" TextColor="White"/>
                    <Button Text="Register" HorizontalOptions="FillAndExpand" BackgroundColor="Gray" TextColor="White" />
              </StackLayout>  
            </StackLayout>            
        </StackLayout>
    </ScrollView>
    </ContentPage.Content>
</ContentPage>
```

The demo shows the following sample screen on iOS.

![](/assets/stacklayout-login-screen.png)

In the above code we also embedded a StackLayout inside another StackLayout and changed the orientation to horizontal for the buttons.


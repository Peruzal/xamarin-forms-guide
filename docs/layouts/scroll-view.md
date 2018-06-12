description: The ScrollView is used to wrap content that needs to scroll. The ScrollView control can only have one child.

# ScrollView

The ScrollView is used to wrap content that needs to scroll. The ScrollView control can only have one child.

> Note, Do not embed a ListView inside a ScrollView as the ListView already can scroll

The contents of the Login page are wrapped inside the ScrollView so that they user can scroll the contents up when the keyboard overlaps the controls.

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




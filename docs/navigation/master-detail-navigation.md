# 

# Master Detail Navigation

The MasterDetailPage is used to create the master and detail relationship type of pages. The one page will act as the master and the other as the detail. The MasterDetailsPage renders independently on each platform. On Android it displays a NavigationDrawer and on iOS it displays on the top left corner and allows the swiping to reveal the menu.

## Create a MasterDetail Page

```csharp
public class MainPageCS : MasterDetailPage
{
    MasterPageCS masterPage;

    public MainPageCS ()
    {
        masterPage = new MasterPageCS ();
        Master = masterPage;
        Detail = new NavigationPage (new ContactsPageCS ());
        ...
    }
    ...
}
```

The Master page usually contains the ListView with the menu items, and the Details contains either a ContentPage, NavigationPage or TabbedPage.

> Note, using any other pages might cause unexpected behaviour.

## Create the Master Page UI in Xaml

```xml
ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="using:MasterDetailPageNavigation"
             x:Class="MasterDetailPageNavigation.MasterPage"
             Padding="0,40,0,0"
             Icon="hamburger.png"
             Title="Personal Organiser">
    <StackLayout>
        <ListView x:Name="listView">
           <ListView.ItemsSource>
                <x:Array Type="{x:Type local:MasterPageItem}">
                    <local:MasterPageItem Title="Contacts" IconSource="contacts.png" TargetType="{x:Type local:ContactsPage}" />
                    <local:MasterPageItem Title="TodoList" IconSource="todo.png" TargetType="{x:Type local:TodoListPage}" />
                    <local:MasterPageItem Title="Reminders" IconSource="reminders.png" TargetType="{x:Type local:ReminderPage}" />
                </x:Array>
            </ListView.ItemsSource>
            <ListView.ItemTemplate>
                <DataTemplate>
                    <ViewCell>
                        <Grid Padding="5,10">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="30"/>
                                <ColumnDefinition Width="*" />
                            </Grid.ColumnDefinitions>
                            <Image Source="{Binding IconSource}" />
                            <Label Grid.Column="1" Text="{Binding Title}" />
                        </Grid>
                    </ViewCell>
                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>
    </StackLayout>
</ContentPage>
```

The page consists of a ListView that's populated with data in XAML by setting its ItemsSource property to an array of MasterPageItem instances. Each MasterPageItem defines Title, IconSource, and TargetType properties.

A DataTemplate is assigned to the ListView.ItemTemplate property, to display each MasterPageItem. The DataTemplate contains a ViewCell that consists of an Image and a Label. The Image displays the IconSource property value, and the Label displays the Title property value, for each MasterPageItem.

## MasterPage Code

The master page will need to expose its ListView so that events can be wired to change the pages :

```csharp
public partial class MasterPage : ContentPage
{
    public ListView ListView => listView;

    public MasterPage()
    {
        InitializeComponent();
    }
}
```

## Creating and Displaying the Detail Page

```csharp
public partial class MainPage : MasterDetailPage
{
    public MainPage ()
    {
        ...
        masterPage.ListView.ItemSelected += OnItemSelected;
    }

    void OnItemSelected (object sender, SelectedItemChangedEventArgs e)
    {
        var item = e.SelectedItem as MasterPageItem;
        if (item != null) {
            Detail = new NavigationPage ((Page)Activator.CreateInstance (item.TargetType));
            masterPage.ListView.SelectedItem = null;
            IsPresented = false;
        }
    }
}
```




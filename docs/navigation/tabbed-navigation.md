description: The TabbedPage is used for tabbed navigation. The layout of the a TabbedPage is dependent on the platform. On Android the tabs are displayed at the top and on iOS at the bottom.

# Tabbed Navigation

The TabbedPage is used for tabbed navigation. The layout of the a TabbedPage is dependent on the platform. On Android the tabs are displayed at the top and on iOS at the bottom.

On iOS the tabs have a `GetIcon` method that can be overridden to load icons from specified source. On Android tabs have a `SetTabIcon` method that allows loading icons from a custom drawable.

## Create a Tabbed Page in Code

The TabbedPage have a Children property. We can assign child objects to the property to add them to the TabbedPage as follows :

```csharp
public class MainPageCS : TabbedPage
{
  public MainPageCS ()
  {
    var navigationPage = new NavigationPage (new SchedulePageCS ());
    navigationPage.Icon = "schedule.png";
    navigationPage.Title = "Schedule";

    Children.Add (new TodayPageCS ());
    Children.Add (navigationPage);
  }
}
```




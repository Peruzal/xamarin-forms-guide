description: Gives the user an indication that something is happening without showing the progress. If you would like to show progress of an activity use the ProgressBar instead.

# Activity Indicator

Gives the user an indication that something is happening without showing the progress. If you would like to show progress of an activity use the ProgressBar instead.

## In XAML

```xml
<ActivityIndicator IsRunning="true" />
```

We can also choose the color as follows :

```xml
<ActivityIndicator IsRunning="true" Color="Fuchsia" />
```

## In Code

```csharp
var activityIndicator = new ActivityIndicator
{
    IsRunning = true,
    Color = Color.Fuchsia
};
```




# Progress Bar

The ProgressBar control is used to dispay progress of an activity.

# In XAML

```xml
<ProgressBar Progress="0.2"  />
```

## In Code

```csharp
var progress = new ProgressBar()
{
    Progress = 0.3
};
```

We could use a platform timer and change the value of the ProgressBar programmatically as follows :

```csharp
public partial class ProgressBarPage : ContentPage
{
    public ProgressBarPage()
    {
        InitializeComponent();
        var progress = new ProgressBar()
        {
            Progress = 0.3
        };

        Content = progress;


        //Start a device timer that fires every 1 second
        Device.StartTimer(TimeSpan.FromSeconds(1),() => {
            if (progress.Progress <= 1)
            {
                // Animate the progress value over 250ms
                progress.ProgressTo(progress.Progress +  0.1, 250, Easing.Linear);  
                return true;
            }
            return false;
        });
    }
}
```
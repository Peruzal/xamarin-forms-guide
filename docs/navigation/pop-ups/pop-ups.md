# Pop Ups

Xamarin.Forms provides support for modal pages. A modal page encourages users to complete a self-contained task that cannot be navigated away from until the task is completed or cancelled. 

They are different types of pop up. 

* Alerts
* Action Sheets
* Modal Page Pop Up

## Alerts

We can display an alert using `DisplayAlert` method on the Page

```csharp
DisplayAlert ("Alert", "You have been alerted", "OK");
```

We can get the result from the alert by assign the return to a variable

```csharp
var result = DisplayAlert ("Delete", "Delete file", "OK", "Cancel");
```

## Action Sheets

Action Sheets let the user choose from a list of options. To display the action sheets we use `DisplayActionSheet`

```csharp
var action = await DisplayActionSheet ("ActionSheet: Send to?", "Cancel", null, "Email", "Twitter", "Facebook");
```

The destroy button is rendered differently than the others, and can be left null or specified as the third string parameter.
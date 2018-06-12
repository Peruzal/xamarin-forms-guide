description: Xamarin.Forms provides support for modal pages. A modal page encourages users to complete a self-contained task that cannot be navigated away from until the task is completed or cancelled. 

# Modal Pop Up

To display a modal pop up we use the the `Navigation` property and call `PushModalAsync`. It will be your responsibility to pop the page off the stack.

```csharp
    var detailPage = new DetailPage ();
    await Navigation.PushModalAsync (detailPage
```

and then in the DetailPage, the page can pop itself from the stack using `PopModalAsync` method of the `Navigation` property.


```csharp
await Navigation.PopModalAsync (); //Dismiss the pop up
```
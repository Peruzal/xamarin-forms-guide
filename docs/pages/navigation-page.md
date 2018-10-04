description: The Navigation class is an import class used for hierachical navigation. The root page is wrapped inside a Navigation page and subsequent pages can be pushed or popped from the stack.

# NavigationPage

The `NavigationPage` is used for hierachical navigation. Pages are pushed and popped onto the stack. You will mainly use the `NavigationPage` in code.

When the root page is wrapped in a `NavigationPage` subsequent pages can be pushed and popped from the stack.

## Add Root Page to NavigationPage

To add the root page to the `NavigationPage` we just need to pass the page in the constructor of the `NavigationPage` as follows :

```csharp
...
// Assign the MainPage of the App to be the NavigationPage
// and have MainPage be the root page of the navigation
MainPage = new NavigationPage(new MainPage());
...
```

With the above code, a navigation bar will be added in an iOS app, and a toolbar in an Android app.
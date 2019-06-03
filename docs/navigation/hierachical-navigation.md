description: The NavigationPage is used for hierarchical navigation. You can push and pop pages. It will automatically manage the stack of pages.

# Hierarchical Navigation

The NavigationPage is used for hierarchical navigation. You can push and pop pages. It will automatically manage the stack of pages.

## Creating a Root Page

You need to initially create a root page, afterwards you can push and pop pages.

```csharp
var rootPage = new NavigationPage(new HomePage());
```

## Pushing a Page

We can use the Navigation property on a ContentPage to push pages as follows :

```csharp
await Navigation.PushAsync(new MoviesPage());
```

The will add the MoviesPage to the stack and navigate to it.

## Popping a Page

A page can be popped from the stack by pressing the back button or the hardware back buttons. Programmatically we can use the PopAsync method on the Navigation property of the ContentPage as follows :

```csharp
await Navigation.PopAsync ();
```

> Note the page that was pushed needs to call PopAsync

## Navigating to the Root Page

We can navigate directly back to the root page using the PopToRootAsync as follows :

```csharp
await Navigation.PopToRootAsync ();
```

## Manipulating the Navigation Stack

We can remove and insert pages in the navigation stack using InsertPageBefore and  RemovePage. E.g after loggin in, we can insert the main page onto the stack and remove the login page as follows :

```csharp
//App.IsLogged = true;
Navigation.InsertPageBefore(new HomePage(), this);
await Navigation.PopAsync();
```
Another way to remove the login page from the navigation stack would be to set a new root page as follows :

```csharp
//App.IsLogged = true;
Application.Current.MainPage = new HomePage();
```
NB: This works well when there's only the login page, otherwise you will need to pop the navigation stack first.

## Passing Data

When can pass data to the new page using a constructor or using data binding.

#### Pass Data Using Constructor

The code below passes in the User object to the HomePage

```csharp
await Navigation.PushAsync(new HomePage(use));
```

#### Pass Data using Data Binding

We can use data binding to pass data into the content page. The data will be available in the new page and the views can use the binding :

```csharp
  var contact = new Contact {
    Name = "Jane Doe",
    Age = 30,
    Occupation = "Developer",
    Country = "USA"
  };

  var secondPage = new SecondPage ();
  secondPage.BindingContext = contact;
  await Navigation.PushAsync (secondPage);
```




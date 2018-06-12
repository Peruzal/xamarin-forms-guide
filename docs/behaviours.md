description: Behaviors lets you add functionality to controls without subclassing them. Instead the functionality is defined separately in a class that inherits from Behavior.

# Behaviors

Behaviors lets you add functionality to controls without subclassing them. Instead the functionality is defined separately in a class that inherits from Behavior.

### Advantages of Using Behaviors

* Behaviors let you de-clutter your code behind files
* Abstract away common that can be used across projects
* They let you add functionality that the control might not have, e.g adding command to controls that do not support.
* Add custom validation to a control, e.g validating an email address in an Entry control
* Add a Command to a ListView ItemSelected Event

When we choose items from a ListView, an ItemSelected event is fired. We would like to add the ability to bind to a command when the ItemSelected event is fired.

## Create the Behavior

We need to sub class the ListView class

```csharp
public class ListItemSelectedBehaviour : Behavior<ListView>
{
}
```

By using the Behavior&lt;T&gt; we can get access to the control's properties. We need to implement two methods that are called on the control, OnAttached and OnDetached and bind the behaviors BindingContext to that of the control as follows :

```csharp
protected override void OnAttachedTo(ListView bindable)
{
    BindingContext = bindable.BindingContext;
    bindable.BindingContextChanged += Bindable_BindingContextChanged;
    bindable.ItemSelected += Bindable_ItemSelected;
}

protected override void OnDetachingFrom(ListView bindable)
{
    base.OnDetachingFrom(bindable);
    bindable.ItemSelected -= Bindable_ItemSelected;
    bindable.BindingContextChanged -= Bindable_BindingContextChanged;
}
```

Basically we need to be able to know when the control's BindingContext changes and also to attach the relevant event. In our case, we are subscribing to the ItemSelected event when the behavior is attached to the control and removing the event when the behavior is detached from the control.

## Add the Relevant Events

We will implement the events and add the relevant code when the above events are fired :

```csharp
void Bindable_ItemSelected(object sender, SelectedItemChangedEventArgs e)
{
    if (e.SelectedItem == null)
    {
    return;
    }
    if (Command.CanExecute(e.SelectedItem))
    {
        Command?.Execute(e.SelectedItem);
    }
    ((ListView)sender).SelectedItem = null;
}

void Bindable_BindingContextChanged(object sender, EventArgs e)
{
    if (sender is BindableObject ListView)
    {
        BindingContext = (sender as BindableObject).BindingContext;
    }
}
```

We are running a Command, lets implement the Command as a property that will be available to the control :

## Add Properties to the Behavior

The following will create a Bindable property of a specific type, in our case, of an ICommand

```csharp
public static BindableProperty CommandProperty = BindableProperty.Create("CommandProperty", typeof(ICommand), typeof(ListItemSelectedBehaviour), null);
```

We also need to define the ICommand property and set and get the values of the bindable property as follows :

```csharp
public ICommand Command {
    get {
        return (ICommand)GetValue(CommandProperty);
    }
    set {
        SetValue(CommandProperty, value);
    }
}
```

Now our ListView have a Command property.

## Attach the Behavior

To attach the behavior we can use the controls collection and add it under the &lt;ListView.Behaviors&gt; as follows :

```csharp
<ListView ItemsSource="{Binding Items}">
    <ListView.Behaviors>
        <local:Behaviours.ListItemSelectedBehaviour Command="{Binding ItemSelectedCommand}" />
    </ListView.Behaviors>
</ListView>
```

We need to add the local prefix in the namespace as follows :

```xaml
xmlns:local="clr-namespace:Demo"
```


Now we write the code for the `ItemSelectedCommand`.
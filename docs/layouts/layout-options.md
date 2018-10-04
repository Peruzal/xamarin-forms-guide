description: Layout Options are used to position the views inside their parents container. Every view has a vertical and horizontal options for setting up its position, size and expansion within the parent.

# Layout Options

Layout Options are used to position the views inside their parents container. Every view has a vertical and horizontal options for setting up its position, size and expansion within the parent.

Only the StackLayout has an expansion property for its views, the other containers will ignore the property.

Available Alignment LayoutOptions

* Start
* Center
* End
* Fill

The default layout options for vertical and horizontal options is **Fill**.

**Start**

For horizontal alignment, Start positions the View on the left hand side of the parent layout, and for vertical alignment, it positions the View at the top of the parent layout.

**Center**

For horizontal and vertical alignment, Center horizontally or vertically centers the View.

**End**

For horizontal alignment, End positions the View on the right hand side of the parent layout, and for vertical alignment, it positions the View at the bottom of the parent layout.

**Fill**

For horizontal alignment, Fill ensures that the View fills the width of the parent layout, and for vertical alignment, it ensures that the View fills the height of the parent layout.

Here is the layout options set for a StackLayout in XAML :

```xml
<StackLayout>
  <Label Text="Start" BackgroundColor="Gray" HorizontalOptions="Start" />
  <Label Text="Center" BackgroundColor="Gray" HorizontalOptions="Center" />
  <Label Text="End" BackgroundColor="Gray" HorizontalOptions="End" />
  <Label Text="Fill" BackgroundColor="Gray" HorizontalOptions="Fill" />
</StackLayout>
```

!!! tip
    A **StackLayout** only respects the **Start**, **Center**, **End**, and **Fill** LayoutOptions fields on child views that are in the opposite direction to the StackLayout orientation. Therefore, child views within a vertically oriented StackLayout can set their **HorizontalOptions** properties to one of the **Start**, **Center**, **End**, or **Fill** fields. Similarly, child views within a horizontally oriented StackLayout can set their **VerticalOptions** properties to one of the Start, Center, End, or Fill fields.

## Expansion and Layout Options

Expansion controls whether the views will take up unused space with the StackLayout when the StackLayout is larger than its views.The space is divided equally by the views that requests expansion by setting the HorizontalOptions and VerticalOptions that uses the suffix _AndExpand_.

!!! tip
    Note that the AndExpand option does not take effect when all the space is used in the StackLayout.
    A StackLayout can only expand views in the direction of its orientation.

A vertically oriented StackLayout can only expands child views that set the `VerticalOptions` property to one of the `StartAndExpand`, `CenterAndExpand`, `EndAndExpand`, `FillAndExpand` and the same for the horizontally oriented StackLayout.

These expansion properties only take effect within a StackLayout :

* StartAndEpand
* CenterAndExpand
* EndAndExapand
* FillAndExpand

> Note that enabling expansion doesn't change the size of a view unless it uses LayoutOptions.FillAndExpand

The following XAML code example demonstrates a vertically oriented StackLayout where each child Label sets its VerticalOptions property to one of the four expansion fields from the LayoutOptions structure:

```xml
<StackLayout Margin="0,20,0,0">
  <BoxView BackgroundColor="Red" HeightRequest="1" />
  <Label Text="Start" BackgroundColor="Gray" VerticalOptions="StartAndExpand" />
  <BoxView BackgroundColor="Red" HeightRequest="1" />
  <Label Text="Center" BackgroundColor="Gray" VerticalOptions="CenterAndExpand" />
  <BoxView BackgroundColor="Red" HeightRequest="1" />
  <Label Text="End" BackgroundColor="Gray" VerticalOptions="EndAndExpand" />
  <BoxView BackgroundColor="Red" HeightRequest="1" />
  <Label Text="Fill" BackgroundColor="Gray" VerticalOptions="FillAndExpand" />
  <BoxView BackgroundColor="Red" HeightRequest="1" />
</StackLayout
```

Each Label occupies the same amount of space within the StackLayout. However, only the final Label, which sets its `VerticalOptions` property to `FillAndExpand` has a different size.


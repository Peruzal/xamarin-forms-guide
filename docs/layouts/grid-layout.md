description: The Grid is used to display views in rows and columns. The Grid rows and columns supports spacing. The Grid is a powerful control. 

# Grid Layout

The Grid is used to display views in rows and columns. The Grid rows and columns supports spacing. The Grid is a powerful control. The control is not ideal for displaying tabular data, for that you should use the [**ListView**](/views/list-view) or the **TableView** control.

The Grid uses the `RowDefinitions` property to define the number of rows in the Grid. It uses the `ColumnDefinitions` to define the number of columns in the Grid.

## Rows and Columns

Row and column information is stored in Grid's **RowDefinitions** & **ColumnDefinitions** properties. RowDefinition has a single property, **Height**, and **ColumnDefinition** has a single property, **Width**. The options for height and width are as follows:

* **Auto** – automatically sizes to fit content in the row or column. Specified as   in XAML.
* **Proportional\(\*\)** – sizes columns and rows as a proportion of the remaining space. Specified as a valu and as \#\* in XAML, with \# being your desired value. Specifying one row/column with \* will cause it to fill the available space.
* **Absolute** – sizes columns and rows with specific, fixed height and width values. Specified as a value and as \# in XAML, with \# being your desired value.

The Grid uses attached properties. This means, views created inside the Grid will have Grid properties but those properties are not defined on those View.

## Spacing

Grid has properties to control spacing between rows and columns. The following properties are available for customizing the Grid:

* **ColumnSpacing** – the amount of space between columns.
* **RowSpacing** – the amount of space between rows.

The following XAML specifies a Grid with two columns, one row, and 5 px of spacing between columns:

```xml
<Grid ColumnSpacing="5">
  <Grid.ColumnDefinitions>
    <ColumnDefinitions Width="*" />
    <ColumnDefinitions Width="*" />
  </Grid.ColumnDefinitions>
</Grid>
```

## Spans

We can use the ColumnSpan and RowSpan to enable views to span over multiple columns or rows.

The following spans the Button over two columns.

```xml
<Button Text = "0" Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2" />
```

##### A Simple Grid

```xml
<Grid>
  <Grid.RowDefinitions>
    <RowDefinition Height="2*" />
    <RowDefinition Height="*" />
    <RowDefinition Height="200" />
  </Grid.RowDefinitions>
  <Grid.ColumnDefinitions>
    <ColumnDefinition Width="Auto" />
    <ColumnDefinition Width="*" />
  </Grid.ColumnDefinitions>
</Grid>
```

We can use the Grid to create complex layouts. The XAML below creates a calculator UI using the Grid layout :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
x:Class="Demo.CalculatorPage"
Title = "Calculator - XAML"
BackgroundColor="#404040">
    <ContentPage.Content>
        <Grid x:Name="controlGrid" RowSpacing="1" ColumnSpacing="1">
            <Grid.RowDefinitions>
                <RowDefinition Height="150" />
                <RowDefinition Height="*" />
                <RowDefinition Height="*" />
                <RowDefinition Height="*" />
                <RowDefinition Height="*" />
                <RowDefinition Height="*" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="*" />
                <ColumnDefinition Width="*" />
                <ColumnDefinition Width="*" />
                <ColumnDefinition Width="*" />
            </Grid.ColumnDefinitions>
            <Label Text="0" Grid.Row="0" HorizontalTextAlignment="End" VerticalTextAlignment="End" TextColor="White"
        FontSize="60" Grid.ColumnSpan="4" />
            <Button Text = "C" Grid.Row="1" Grid.Column="0"
        BackgroundColor="#ddd" TextColor="Black" BorderRadius="0" FontSize="40" />
            <Button Text = "+/-" Grid.Row="1" Grid.Column="1"
        BackgroundColor="#ddd" TextColor="Black" BorderRadius="0" FontSize="40" />
            <Button Text = "%" Grid.Row="1" Grid.Column="2"
        BackgroundColor="#ddd" TextColor="Black" BorderRadius="0" FontSize="40" />
            <Button Text = "div" Grid.Row="1" Grid.Column="3"
        BackgroundColor="#E8AD00" TextColor="White" BorderRadius="0" FontSize="40" />
            <Button Text = "7" Grid.Row="2" Grid.Column="0" BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "8" Grid.Row="2" Grid.Column="1"
        BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "9" Grid.Row="2" Grid.Column="2"
        BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "X" Grid.Row="2" Grid.Column="3"
        BackgroundColor="#E8AD00" TextColor="White" BorderRadius="0" FontSize="40"  />
            <Button Text = "4" Grid.Row="3" Grid.Column="0"
        BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "5" Grid.Row="3" Grid.Column="1"
        BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "6" Grid.Row="3" Grid.Column="2"
        BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "-" Grid.Row="3" Grid.Column="3"
        BackgroundColor="#E8AD00" TextColor="White" BorderRadius="0" FontSize="40"  />
            <Button Text = "1" Grid.Row="4" Grid.Column="0"
        BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40"/>
            <Button Text = "2" Grid.Row="4" Grid.Column="1"
        BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "3" Grid.Row="4" Grid.Column="2"
        BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "+" Grid.Row="4" Grid.Column="3"
        BackgroundColor="#E8AD00" TextColor="White" BorderRadius="0" FontSize="40"  />
            <Button Text = "0" Grid.ColumnSpan="2"
        Grid.Row="5" Grid.Column="0" BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "." Grid.Row="5" Grid.Column="2"
        BackgroundColor="#eee" BorderRadius="0" TextColor="Black" FontSize="40" />
            <Button Text = "=" Grid.Row="5" Grid.Column="3"
        BackgroundColor="#E8AD00" TextColor="White" BorderRadius="0" FontSize="40"  />
        </Grid>
    </ContentPage.Content>
</ContentPage>
```




# DatePicker

The view allows selecting a date. The control allows limiting the minimum and maximum date ranges that can be selected.

## Define in XAML

```xml
DatePicker />
```

### Limit the Date Range

We can format and also limit the date range in XAML as follows :

```xml
<DatePicker Format="MM-dd-yyyy" MinimumDate="02-24-2018" MaximumDate="02-28-2018" />
```

## Define in Code

```csharp
var startDatePicker = new DatePicker
{
    Format = "MM-dd-yyyy",
    Date = DateTime.Now.Date.AddDays(-1),
    MinimumDate = DateTime.Parse("02-01-2018"),
    MaximumDate = DateTime.Parse("02-28-2018")
};
```




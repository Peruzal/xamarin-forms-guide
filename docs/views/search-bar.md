# SearchBar

The view provides a search box.

## In XAML

```xml
<SearchBar Placeholder="{Binding SearchPlaceholder}" Text="{Binding SearchTerm}" SearchCommand="{Binding SearchBarCommand}" SearchCommandParameter="Albania" VerticalOptions="Start" />
```

## In Code

```csharp
Command<object> _searchBarCommand;
public Command<object> SearchBarCommand 
{
    get {
        return _searchBarCommand ?? ( _searchBarCommand = new Command<object>(Search));        
    }
}
```

The SearchCommand is bound to the Search so that it can filter the contents of the ListView. The complete code is as follows :

```csharp
public class SearchBarViewModel : BaseViewModel
{
    public SearchBarViewModel()
    {
        Countries = new ObservableCollection<string>(){
            "Afghanistan", "Albania", "Algeria", "Andorra", "Angola", "Antigua and Barbuda", "Argentina"
        };
    }

    Command<object> _searchBarCommand;
    public Command<object> SearchBarCommand 
    {
        get {
            return _searchBarCommand ?? ( _searchBarCommand = new Command<object>(Search));
        }
    }

    public ObservableCollection<string> Countries { get; set;}

    public string SearchTerm { get; set; }
    public string SearchPlaceholder {
        get {
            return "Country name to search";
        }
    }

    private void Search(object searchTerm)
    {
        var searchWord = searchTerm as string;
        if (!string.IsNullOrEmpty(searchWord))
        {
            var countries = Countries.Where(s => s.Equals(searchWord));
            Countries = new ObservableCollection<string>(countries);
            OnPropertyChanged("Countries");
        }
    }
}
```

> Note this code is not complete, it just shows how the SearchBarCommand is bound to the SearchBar control.
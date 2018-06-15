# Dependency Injection

`DependencyService` allows apps to call into platform-specific functionality from shared code. This functionality enables Xamarin.Forms apps to do anything that a native app can do.

`DependencyService` is a dependency `resolver`. In practice, an interface is defined and DependencyService finds the correct implementation of that interface from the various platform projects.

## Setting Up DependencyService

Xamarin.Forms apps need four components to use `DependencyService` :

* **Interface** – The required functionality is defined by an interface in shared code.
* **Implementation** Per Platform – Classes that implement the interface must be added to each platform project.
* **Registration** – Each implementing class must be registered with DependencyService via a metadata attribute. Registration enables DependencyService to find the implementing class and supply it in place of the interface at run time.
* **Call to DependencyService** – Shared code needs to explicitly call DependencyService to ask for implementations of the interface.

!!! danger 
    Note that implementations must be provided for each platform project in your solution. Platform projects without implementations will fail at runtime.

## Interface Definition

The interface is defined in the Xamarin Forms project. We are going to define an interface to get the path for the SQLite database. Each platform will need to provide the concrete implementation.

*IFileHelper.cs*

```csharp
public interface IFileHelper
{
    string GetLocalPath(string filename);
}
```

### Implementation 

On each platform we need to provide the implementation for the interface definition.

### Android Implementation

This code goes in the Android project.

*FileHelper.cs*
```csharp
public class FileHelper : IFileHelper
{
    public string GetLocalPath(string filename)
    {
        var documentsFolder = Environment.GetFolderPath(Environment.SpecialFolder.Personal);
        return Path.Combine(documentsFolder, filename);
    }
}
```

### iOS Implementation

This code goes in the iOS project.

*FileHelper.cs*
```csharp
public class FileHelper : IFileHelper
{
    public string GetLocalPath(string filename)
    {
        //Get path of the document folder
        var documentFolder = Environment.GetFolderPath(Environment.SpecialFolder.Personal);
        //Get path of the Library folder
        var libraryFolder = Path.Combine(documentFolder, "..", "Library", "Databases");
        if (!Directory.Exists(libraryFolder))
        {
            Directory.CreateDirectory(libraryFolder);
        }
        return Path.Combine(libraryFolder, filename);
    }
}
```


## Registration

Each implementation of the interface needs to be registered with DependencyService with a metadata attribute. The following code registers the implementation for iOS :

```csharp
[assembly: Dependency(typeof(FileHelper))]
namespace DataBindingDemo.iOS
{
    public class FileHelper : IFileHelper { ... }
}
``` 

and for Android :

```csharp
[assembly: Dependency(typeof(FileHelper))]
namespace DataBindingDemo.Droid
{
    public class FileHelper : IFileHelper { ... }
}
```

## Call to DependencyService

Once the project has been set up with a common interface and implementations for each platform, use DependencyService to get the right implementation at runtime :

```csharp
// Resolve the FileHelper
var fileHelper = DependencyService.Get<IFileHelper>();
```

!!! note
    Using `DependencyService.Get<IFileHelper>()` we can resolve the platform specific code for the `FileHelper`. On iOS it will call the iOS specific `FileHelper` code and on Android, it will resolve to the Android specific `Filehelper` code we defined.
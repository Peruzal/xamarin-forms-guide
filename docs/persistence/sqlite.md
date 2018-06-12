description: The SQLite database is the most popular relational database on mobile devices.

# SQLite.NET

The SQLite database is the most popular relational database on mobile devices.

## Install the library

To work with SQLite database you will need to install the `sqlite-net-pcl` Nuget package in both the PCL and Android and iOS projects.


## Database file path on Android and iOS

The database is stored in different location on Android and iOS. We will need to write code in each of the native projects and use the `DependencyService` to resolve the path during runtime on each platform.

We will use an interface that we will implement on each native project.

### Define the interface in the PCP project

Define the interface in the PCL project 

*IFileHelper.cs*

```csharp
public interface IFileHelper
{
    string GetLocalPath(string filename);
}
```

**Implement the interface on Android**

*Filehelper.cs*

```csharp
[assembly: Dependency(typeof(FileHelper))]
namespace DataBindingDemo.Droid
{
    public class FileHelper : IFileHelper
    {
        public string GetLocalPath(string filename)
        {
            var documentsFolder = Environment.GetFolderPath(Environment.SpecialFolder.Personal);
            return Path.Combine(documentsFolder, filename);
        }
    }
}
```

!!! note
    The files are kept on the apps files folder on Android. To register the class with the `DependencyService` we use the `assembly` attribute and specify the file name using `[assembly: Dependency(typeof(FileHelper))]`. We do the same on iOS as well. Note that the attribute needs to be above the namespace definition.

***Implement the interface on iOS*

*FileHelper.cs*

```csharp
[assembly: Dependency(typeof(FileHelper))]
namespace DataBindingDemo.iOS
{
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
}
```

On iOS, user files are kept in the `Library` folder. We first need to get the path of the `Documents` folder and then navigate to the `Library` folder. We register the class with the `DependencyService` the same way as on Android using the `[assembly: Dependency(typeof(FileHelper))]`.

On we have provided the implementation in each project, we can now resolve the class during runtime.


## Create Database

To create the database connection we use the `SqliteConnection` and require a path. So we will use the `DependencyService` to resolve the path on the platform on which we are running on.

```csharp
// Resolve the FileHelper
var fileHelper = DependencyService.Get<IFileHelper>();
if (fileHelper != null)
{
    var databasepath = fileHelper.GetLocalPath("chats.db");
    var conn = new SQLiteConnection(databasepath);
}
```

Using `DependencyService.Get<IFileHelper>()` we can resolve the platform specific code for the `FileHelper`. On iOS it will call the iOS specific `FileHelper` code and on Android, it will resolve to the Android specific `Filehelper` code we defined.

## Create a Table

To create the table you use the `CreateTable<T>` generic method of the connection as follows :

```csharp
var conn = new SQLiteConnection(databasepath);
var id = conn.CreateTable<ChatMessage>();
Debug.WriteLine(id);
``` 

If the table exists its not created. The return will be zero for a successful table creation.

## Insert data

We use the `Insert` method to insert new data into the table. SQLite.net will figure out the type and insert the data into the correct table. To insert data into out chat table, we can do the the following:

```csharp
_conn.Insert(new ChatMessage()
{
    FromId = "josephk",
    ToId = "#general",
    Message = MessageEntry.Text,
    HasAttachments = false
});
```

## Retrieve data from a table

We can query the table using the generic method `Table<T>` on the connection object. E.g. to return all the records in the chat, we can do the following :

```csharp
var results = _conn.Table<ChatMessage>();
results.ForEach((ChatMessage msg) =>
{
    Debug.WriteLine($"{msg.Id} {msg.Message}");
});
```

We can also use LINQ and perform some filters on the returned data. E.g. to return all messages with attachments :

```csharp
var results = _conn.Table<ChatMessage>().Where(msg => msg.HasAttachments);
```

## Delete a record

We can use the `Delete` method to remove a record from the table.

```csharp
 _conn.Delete<ChatMessage>(1)
```

The `1` is the primary key. We can also pass in the object to be deleted instead of its primary key.


## Update table data

We can use the `Update` method to update an existing record.

## Asynchronous methods calls

The SQLite.net library also supports the asynchronous methods for creating the database, querying, updating and deleting methods.

* `SQLiteAsyncConnection`
* `InsertAsync`
* `UpdateAsync`
* `DeleteAsync`
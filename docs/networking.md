description: We can data from a remote API using HTTP. Using REST API we can get and create data.

# Networking

We can data from a remote API using HTTP. Using REST API we can get and create data.

## Permission

**Android**

To make network calls on Android you will need to have the `INTERNET` permission. On the Android project, add the following permission in the `AndroidManifest.xml`  `<uses-permission android:name="android.permission.INTERNET" />`.

**iOS**

On iOS you will just need to make sure that the API is using `https`. If the url is `http`, you will need to add some configuration to the `Info.plist` file.

## Performing a *GET* Request

Let's retrieve a random joke from the API url `http://api.icndb.com/jokes/random`. We use the `GetStringAsync` method of the `HttpClient` class as follows :

```cs
using (var client = new HttpClient()) {
    var content = await client.GetStringAsync("http://api.icndb.com/jokes/random");
    Console.WriteLine(content);
}
```

## Performing a POST Request

To send data to the server you use the HTTP form data and send the parameters as form url encoded using the `FormUrlEncodedContent` class. The parameters will be sent as key/value pairs. We use the `PostAsync` method of the `HttpClient` class.

```cs
using (var client = new HttpClient())
{
    client.BaseAddress = new Uri("http://api.peruzal.com/");
    //Create a list of params
    var content = new FormUrlEncodedContent(new[]
    {
        //The parameters to post, in a key/value pair
        new KeyValuePair<string, string>("title", "Dawn of the Planet Earth"),
        new KeyValuePair<string, string>("category", "Sci-Fi")
    });

    //Make the network call to post
    var result = await client.PostAsync("/api/movie", content);
    string resultContent = await result.Content.ReadAsStringAsync();
    Console.WriteLine(resultContent);
}
```

## Post JSON

Instead of sending the content as form url encoded, we can post the body of the content as JSON as follows:

```csharp
var content = new StringContent(jsonObject.ToString(), Encoding.UTF8, "application/json");
var result = await client.PostAsync(url, content).Result;
```

## Posting form data

We can post form data using the `FormUrlEncodedContent` as follows:

```csharp
var content = new FormUrlEncodedContent(new List<KeyValuePair<string, string>>()
{
    new KeyValuePair<string, string>("username", entryUsername.Text),
    new KeyValuePair<string,string>("password", entryPassword.Text)
}); 

var result = await client.PostAsync(url, content);
```

## Send Headers

To send the headers, we add the headers as a key value pair in the `DefaultRequestHeaders` collection as follows :

```csharp
private Task<string> fetchMovies(){
    var client = new HttpClient();
    //Add the header as a key value pair
    client.DefaultRequestHeaders.Add("X-Parse-Application-Id", "Value of header here");
    return client.GetStringAsync("https://parse.peruzal.com/parse/classes/Movie/");
}
```

!!! note
    The header name is `X-Parse-Application-Id` and the value of the header is `Value of header here`.
description: Using the Xamarin.Essentials library we can store preferences for each platform using a common api.

# Preferences

Using the Xamarin.Essentials library we can store preferences for each platform using a common api.

## Install the Xamarin.Essentials 

At the time of writing the Xamarin.Essentials library is still in preview. You will need to enable install pre-release nuget packages.

## Set Preference

To set the preferences, you we use the the `Set` method. The key is a string and the value could be any value type.

```csharp
 Preferences.Set("nickname", "Joseph");
```

## Read Preference

To read the preference, we use the `Get` static method of the `Preference` class as follows :

```csharp
 var nickname = Preferences.Get("nickname", string.Empty);
```

You will need to pass a default value if the preference is not found.

## Remove the Preference

Use the `Remove` method and pass in the key.

```csharp
Preferences.Remove("nickname");
```

## Remove all Preferences

We can use the `Clear` method to remove all the preferences set.

## Named Preferences

On Android, if we do not provide a name when setting to getting the preferences, the default preferences are used. We can alternatively provide a name when setting and getting the preferences.

```csharp
Preferences.Set("nickname", "Joseph", "private_prefs");
```

On iOS, a named `StandardUserDefaults` file we be created to store the named preferences.
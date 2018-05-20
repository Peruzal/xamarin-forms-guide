# Entry

![Entry View](../images/views/entry.png)

The `Entry` view is used for entering a single line of text. It is best used for collecting small amounts of text like usernames and passwords. It can be configured to displayed different types of keyboards.

## Define in XAML

```xml
<Entry Placeholder="Username" />
```

## Define in Code

```csharp
var entry = new Entry {
    Placeholder = "Username"
};
```

## Configure Password

We can hide the characters in the Entry so it displays black circles and hides its contents using the `Password` property in code and `IsPassword` in XAML as follows :

In XAML

```xml
<Entry Placeholder="Password" IsPassword="true" />
```

In Code

```csharp
var entry = new Entry {
    Placeholder = "Username",
    IsPassword = true
};
```

## Disable Entry

We can disable the Entry field using the `IsEnabled` property as follows :

```xml
<Entry IsEnabled="false" Text="This is a disabled entry" />
```

## Configure Keyboards

We can use the Keyboard property to configure what sort of keyboard is shown for the Entry view. The options are :

* **Default** – the default keyboard
* **Chat** – used for texting & places where emoji are useful
* **Email** – used when entering email addresses
* **Numeric** – used when entering numbers
* **Telephone** – used when entering telephone numbers
* **Url** – used for entering file paths and web addresses

In XAML

```xml
<Entry Placeholder="Username" Keyboard="Email" />
```

In Code

```csharp
var entry = new Entry{
    Placeholder = "Username",
    Keyboard = Keyboard.Email
};
```

## Change Text Color

We can use the `TextColor` property to change the color of the text.

```xml
<Entry TextColor="#E64A19" Placeholder="Username" />
```

and we can achieve the same in code as follows :

```csharp
var entry = Entry { 
    TextColor = Color.FromHex ("#77d065"), 
    Text = "Xamarin Green" 
};
```

## Change Font Size

We can use the `FontSize` property to change the font size of the text :

```xml
<Entry FontSize="Large" Placeholder="Large Font" />
```
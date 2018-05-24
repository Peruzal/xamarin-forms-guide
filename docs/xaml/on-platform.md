# Platform Specific

When you want to render your UI differently on each platform you can use the `OnPlatform` XAML extension to run code for Android, iOS and UWP. An example is, on iOS, the content shows up right from the top and you might want to push it downloads 20points, but on Android and UWP content is displayed after the status bar or tool.

## Apply Margin Per Platform

Lets apply a 20 point margin for all platforms :

```xml
<StackLayout Margin="0,20,0,0">
    <Label Text="This will be 20 points below the status bar on iOS" />
</StackLayout>
```

`Margin` is of type `Thickness`. The value are as follows :

* **First zero** -  Left margin
* **20** - Top margin
* **Third zero** - Right margin
* **Last zero** - Bottom margin

But we ideally want is to only apply the top margin only on iOS. To accomplish that we would use the `OnPlatform` property as follows :

```xml
<StackLayout>
    <StackLayout.Margin>
        <OnPlatform x:TypeArguments="Thickness">
            <On Platform="iOS" Value="20" />
        </OnPlatform>
    </StackLayout.Margin>
<Label Text="This will be 20 points below the status bar on iOS" />
</StackLayout>
```

Since `Margin` is a complex structure, we open a tag for it in XAMl beginning with `<StackLayout.Margin>` and now specify that we need to apply different values for each platform using the `OnPlatform`. We also specify what type of value we need to apply, in this case margin is of type `Thickness`.

We then define the values for each platform, in this case we only wanted to apply for iOS, the other platforms would be on default 0.

We can also use a shortened syntax to apply the margin, e.g. to apply a margin of 20 on iOS we can do the following :

```xml
<StackLayout>
    <StackLayout.Margin>
        <OnPlatform x:TypeArguments="Thickness" iOS="20" />
    </StackLayout.Margin>
<Label Text="This will be 20 points below the status bar on iOS" />
</StackLayout>
```

We can use the same syntax to apply for Android and iOS both as follows :

```xml
<StackLayout>
    <StackLayout.Margin>
        <OnPlatform x:TypeArguments="Thickness" iOS="20" Android="20" />
    </StackLayout.Margin>
<Label Text="This will be 20 points below the status bar on iOS" />
</StackLayout>
```

### Apply Different Margins for each Platform

If we wanted to apply different margins for Android and iOS, we could have done the following :

```xml
<StackLayout>
    <StackLayout.Margin>
        <OnPlatform x:TypeArguments="Thickness">
            <On Platform="iOS" Value="20" />
            <On Platform="Android" Value="10" />
        </OnPlatform>
    </StackLayout.Margin>
</StackLayout>
```

The margin would be 20 for iOS and 10 for Android for all the sides.


## Change Margin with Code

In code, we would use a `switch` statement and check the `Device.RuntimePlatform` as follows :

```csharp
switch(Device.RuntimePlatform){
    case Device.iOS:
        Content.Margin = 20;
        break;
    case Device.Android:
        Content.Margin = 10;
        break;
}
```
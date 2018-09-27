description: Xamarin Forms is a UI framework that is used to develop native cross platform mobile apps for Android, iOS and Windows UWP using C# programming language.

# Developing Android and iOS Mobile Apps with Xamarin Forms

![Xamarin Forms](images/xamarin-forms.png)

## What is Xamarin Forms
Xamarin Forms is a UI framework that is used to develop native cross platform mobile apps for Android, iOS and Windows UWP using C# programming language.

Visual Studio is the primary IDE(Integrated Development Environment) used for developing Xamarin Forms applications.

## Why choose Xamarin Forms
- One language to rule them all, **C#**. You don't need to learn Java and Kotlin for Android or Objective-C and Swift for iOS.
- Save cost. See below how much it would cost to develop a typical app for both Android and iOS.
- Quick to market. With Xamarin Forms, you develop once and deploy to both platforms.

![Xamarin Cost Savings](images/xamarin-cost-savings.png)

## When not to use Xamarin Forms

- When you need pixel perfect apps, Xamarin Forms is not the tool to use.
- Xamarin Forms is not good for building games
- Apps that depend with a lot of native functionality for one platform are not good candidates for developing Xamarin Forms applications.

## History
Xamarin was found by Nat Friedman, Miguel de Icaza and Joseph Hill in May 2011 and was later bought by Microsoft in 2016.

Xamarin Studio was used on Mac and a separate plugin for Visual Studio was used to develop on Wndows. 

When Microsoft purchased Xamarin they made Xamarin open source and removed payment options. This helped the adoption of Xamarin.

Microsoft then integrated Xamarin into Visual Studio. You can now develop on both Windows and Mac with Visual Studio for Windows and Visual Studio for Mac.

## Why was Xamarin not Popular
Although a powerful platform, Xamarin was not widely known compared to the other cross platform development tools, and here are some of the reasons:

- Xamarin license for each platform, one for Android and another for iOS
- Xamarin Visual Studio plugin license
- Single developer license

Before the acquisition by Microsoft, Xamarin was licensed per platform per developer. You would need two licenses to develop both Android and iOS and another license to use Xamarin for Visual Studio. If you used both a Mac and a PC you would need in total 4 licenses. This was really expensive and only corporates could afford to spend that much money on licensing the software.

## Platforms
Xamarin Forms is available on both Windows and Mac OS. You can build Xamarin Forms applications using Visual Studio on Windows and Visual Studio for Mac on OS X.

## What is Traditional Xamarin Development?
![Traditional Xamarin Forms](images/xamarin-platform-specific.png)
The traditional approach also called the silo approach to Xamarin development is to develop the UI natively for each platform and share business logic.

This is different to Xamarin Forms approach. With Xamarin forms, you share the UI code and also the business logic.


## Which Xamarin approach is best for your app?

### Xamarin.Forms is best for

* Apps where code sharing is more important than custom UI
* Apps that require little platform-specific functionality
* Developers comfortable with XAML

### Xamarin.iOS & Xamarin.Android are best for:

* Apps with interactions that require native behavior
* Apps that use many platform-specific APIs
* Apps where custom UI is more important than code sharing
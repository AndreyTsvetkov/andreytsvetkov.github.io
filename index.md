---
layout: page
---
# Creating software. 13 years up to now. 

![](http://blog.salihulukoylu.com/wp-content/uploads/2015/10/sql2.fw_-60x60.png){:class="skill"}
Started from Delphi and C++ Builder, got involved into the **.NET**-development from the times of .NET 1.0 up until now. Since then, **C#** is my old best friend. Tons of code written,  mostly in Visual Studio, from oldschool WinForms and WebForms, WPF and Silverlight to Windows Phone and Windows 10, **ASP.NET MVC** and ASP.NET Core. 

![](http://www.bestrong.org.gr/pictures/xs/xs_4467_l.png){:class="skill"}
I have everlasting romance with functional languages. Having fun with **F#**, **Scala**, Elm, even some Haskell. But day-to-day functional experience goes from C#, heavily using Linq and other libs like my [Functional.Maybe](https://github.com/AndreyTsvetkov/Functional.Maybe).  


![](https://cdn-images-1.medium.com/fit/c/60/60/1*qp4ypiTAjg5aTLwaxvx91w.png){:class="skill"}
The **TypeScript**'s appearance changed my relationships with the frontend. Now it is another home environment for me. Contemporary frontend technologies are  very inspiring, so through Backbone, Knockout &c I shifted to **React** & MobX, trying to build more concise and modular components.

![](http://www.orangesystem.ru/upload/iblock/df8/df83781a0b82b2f35f080e3664e43b1c/f47802578875ab2ef9e1fa83be680f08.png){:class="skill"}
And all the traditional stuff, of course - relational databases (MSSQL), queue services (RabbitMQ & others), nosql storages (ElasticSearch & others). 

## My projects

In 2016 I started to participate more actively in the open source development. My `Functional.Maybe` library as a nuget package was installed more than 5K times, downloaded about 5 times a day. 


#### Functional.Maybe | [github](https://github.com/AndreyTsvetkov/Functional.Maybe) | ![Build status](https://ci.appveyor.com/api/projects/status/8e2bdbu4q60vu2o5?svg=true) | [nuget](https://www.nuget.org/packages/Functional.Maybe/)

This library introduces the `Maybe<T>` type (like F-languages Option type), closely integrated into .net ecosystem, including linq query syntax. Rich extension API allows to write declarative code in many scenarios where previously you needed a tree of if-else statements. 

<table>
    <tr>
        <td>This code</td>
        <td>becomes this</td>
    </tr>
    <tr>
        <td>
{% highlight C# %}
if (userId != null) 
{
    var user = repo.FindById(userId);
    if (user != null) 
    {
        var notifications = user.Notify();
        foreach (var n in notifications)
        {
            _notifier.Send(n);
        }
    }
}
{% endhighlight %}            
        </td>
        <td>
{% highlight C# %}
userId.ToMaybe()
    .SelectMany(repo.FindById)
    .Select(user => user.Notify())
    .Do(notifications => 
        notifications.ForEach(_notifier.Send));
{% endhighlight %}            
        </td>
    </tr>
</table>

For more samples see [project readme](https://github.com/AndreyTsvetkov/Functional.Maybe/blob/master/Readme.md).

#### fast-nuget-update | [github](https://github.com/AndreyTsvetkov/fast-nuget-update ) | [![Build status](https://ci.appveyor.com/api/projects/status/ckwopqwiws29cxmn?svg=true)](https://ci.appveyor.com/project/AndreyTS/fast-nuget-update) | [download](https://github.com/AndreyTsvetkov/fast-nuget-update/releases)

Simple tool to bulk update nuget package references for Visual Studio projects (useful for huge solutions). 

This call updates all the references to Nuget package `MyPackage` to version `1.3.1` in all the `*.csproj` files in the current folder: 

    fast-nuget-update --name MyPackage --version 1.3.1

It takes several seconds even on 100 projects, compared to ≈30minutes of Visual Studio.  


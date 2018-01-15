---
layout: page
---
# Обо мне

14 лет в профессии. Анализирую процессы, выявляю проблемы, решаю их с помощью головы и программного обеспечения.

## Моё дело

Я работаю как независимый консультант по автоматизации и разработчик программного обеспечения. Я анализирую проблемы и задачи моих клиентов, и если они решаются с помощью автоматизации, я предлагаю и реализую программное решение, которое делает организацию лучше, четче и более управляемой. 

У меня есть команда, которая может создавать качественный продукт, я управляю ей как архитектор и тимлид и отвечаю за результаты ее работы.

Такая работа предполагает глубокое погружение в дела клиента, полное доверие и долю от результата. Поэтому я очень тщательно выбираю проекты, и могу себе позволить работать только с теми клиентами, с которыми есть хороший личный контакт, потому что эти отношения имеют тенденцию перерастать в партнерские. 

## История развития

На факультете Кибернетики в МИФИ я получил начальный импульс к изучению программирования в широком спектре технологий, но специализировался дальше на мире `.NET`, начав работу с ним с момента появления этого стека. Прошел вместе с платформой весь её путь, от C#1.0, включая Windows Forms, WPF & Silverlight, и, прежде всего, `ASP.NET` от Web Forms до `MVC Core`, и далее. 

Чтобы не увязнуть в одном мире и одном взгляде, всегда изучал концепции из разных направлений. Познакомился и полюбил функциональное программирование: `Haskell`, `Scala`, `F#`. Сейчас многие аспекты ФП занимают важное место в текущей практике на C#. Популярностью на NUget пользуется моя реализация option type [Functional.Maybe](https://github.com/AndreyTsvetkov/Functional.Maybe). 

Фронтэнд наконец проснулся и стал давать интересные технологии и подходы. `TypeScript` открыл путь для качественного программирования на клиенте. `React` и библиотеки управления состоянием, например `MobX`, сделали для меня программирование на клиенте не менее красивым и вдохновляющим, как и на сервере.  

### Главное — в голове

По мере накопления опыта становится ясно, что конкретные технологии второстепенны по отношению к подходам и концепциям. Сначала ты в изучении опираешься на выработанные шаблоны (OOP Principles, Patterns), потом интериоризируешь их в своем сознании как принципы (DRY, SOLID), пока они не переходят в область неосознанной компетенции и не становятся частью твоего повседневнего мышления. 



<!-- 
# Last blog posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul> -->

# Open source


## Functional.Maybe | [github](https://github.com/AndreyTsvetkov/Functional.Maybe) | ![Build status](https://ci.appveyor.com/api/projects/status/8e2bdbu4q60vu2o5?svg=true) | [nuget](https://www.nuget.org/packages/Functional.Maybe/)

**20К+** установок. **13** установок в день.

Одна из реализацией типа `Maybe<T>` (Option type из мира ФП), качественно интегрированный с экосистемой .net, включая linq query. Богатый набор методов-расширений позволяет писать декларативный код во мноих сценариях. 

<table class="narrow-figure">
    <tr>
        <td>Это дерево</td>
        <td>Превращается в линейную цепочку</td>
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

Примеры см. на [сайте проекта](https://github.com/AndreyTsvetkov/Functional.Maybe/blob/master/Readme.md).

---

## fast-nuget-update | [github](https://github.com/AndreyTsvetkov/fast-nuget-update ) | [![Build status](https://ci.appveyor.com/api/projects/status/ckwopqwiws29cxmn?svg=true)](https://ci.appveyor.com/project/AndreyTS/fast-nuget-update) | [download](https://github.com/AndreyTsvetkov/fast-nuget-update/releases)

Утилита для обновления версий пакетов в большом решении Visual Studio.

Вот такой вызов обновляет все версии ссылок на пакет `MyPackage` на версию `1.3.1` во всех `*.csproj` файлах в текущей папке: 

    fast-nuget-update --name MyPackage --version 1.3.1

Это занимает несколько секунд на 100 проектах, в сравнении с получасом в Visual Studio.  


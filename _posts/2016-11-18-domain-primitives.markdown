---
layout: post
title:  "domain-primitives"
caption: "Domain Primitives"
date:   2016-11-22 11:00:00 +0300
categories: ddd csharp value-type
---

I believe the more relevant facts about our Domain Model are directly represented in domain classes, the better. 

But we often tend to keep them "in the mind" instead of writing down in code.

## Too primitive types

One common mistake is misusing of primitive types as representation of custom domain value types. For intance, generic `int` instead of specific `enum UserRights`. 

Let's take an example. Assuming our code operates with some location descriptors looking like `"city-48"`. One could (mistakenly in many cases) use `string` instead of creating some custom `LocationId` Value Object.

Then his code starts being polluted by multiple checks he needs to do to ensure the data passed are correct: 

```
... void SomeCode(string locId) 
{
    if (locId == null && !locId.Contains("-")) 
     // this check is not even complete!
    {
        throw new ArgumentException(nameof(locId));
    }
    ...
}
```

So it starts to violate DRY, as these checks appear now and then. And also it violates the strong typization, as it becomes possible to represent incorrect data in a perfectly compilable way. 

## Making things clear

The better way is to say clearly we deal with some LocationId value. 

```
... void SomeCode(LocationId id) 
{
    // no check here, but code is more safe now, not less!
    ...
}
```


This class should be not-nullable, if language or infrastructure allows this. In C# it can be `struct` where `struct` fits good, or I have some [custom approach for non-nullable ref types](#not-written-yet) when `struct` is not an option. 

Of course, in any case, `struct` or not, it should be **immutable** type with [Value Object](http://martinfowler.com/bliki/ValueObject.html) semantics:

```

enum LocationType { Country, City }

struct LocationId : IEquatable<LocationId>
{
    private readonly LocationType _type;
    private readonly int _id;

    public LocationId(LocationType type, int id) 
    {
        _id = id;
        _type = type;
    }

    public override string ToString() => $"{_type}-{_id}";
    ... 
}

```

## So what?

Now we have one class more, plenty of trash-checks less and compile-time code verification more complete. 

More, we have more domain *knowlendge* directly represented in the code, therefore more *value* put into our git repository. 
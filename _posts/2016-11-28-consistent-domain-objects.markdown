---
layout: post
title:  "consistent-domain-objects"
caption: "Consistent Domain Objects"
date:   2016-11-28 11:00:00 +0300
categories: ddd 
---

We model the domain with our classes. Thus we must ensure that it is impossible to create an object in an incorrect state. It is the constructor which helps us with it. 

But what does the constructor call means from the purpose of domain? In reality an object is created only once and then exists continuously until it is destroyed somehow. But in our code we have some serialization, deserialization, storing and getting from DB — all that things have no connection with the domain. 

## Value objects

For immutable [value objects](http://martinfowler.com/bliki/ValueObject.html), we consider them to "exist already". We do not really 'create' the `5` number, or the `red` color value — all of them just are part of their type values set, and as a concept, `5` lives eternally. So we just build a representation of it in memory, and it is the first meaning of the constructor call: technically create the in-memory object as a representation of already existing Domain Object (value object in this case). 

```csharp

var date = new Date(2000, 07, 15); // now date references the '15 Jul 2000'; 
// of course, this 'new' does not model some real creation in the domain. 

```

## Entities

On the contrary, for entities, which have domain-defined life cycle, we are going to create brand-new entities objects, which did not exist before. New customer registered, new order created etc.

### "Business-aware" new

Let's say we work with domain 'Education planning system', so we have Course and can plan Lessons for this course, and assign Students for them.

```csharp
var lesson = new Lesson(course, dateTime); 
```

When the lesson is planned, according to the business process, no teacher or students are assigned. For some period of its lifetime the lesson justs sits there in the schedule, waiting if someone would like to study at that specific time. If some student does, he is assigned to the lesson:

```csharp
var studentResult = lesson.TryAssignStudent(student);
var teacherResult = lesson.TryAssignTeacher(teacher);
```

### "Technical" new

It means that to restore our object from database, we need to set not only the course and datetime (as in the primary constructor), but also the list of students and an optional teacher. The code of data layer component which should create the lessons would look like:

```csharp
var lesson = new Lesson(course, dateTime, students, teacher); 
```

Such constructor does not makes sense for domain code, as domain expert never says "we plan a lesson for the course at the date and time with empty set of students and None teacher", he just says "we plan a lesson for the course at the date and time". 

When one uses Event Sourcing, this re-creation constructor would be like this:

```csharp
var lesson = new Lesson(lessonEvents);
```

And again it makes sense only in technical context, leaving the 
"domain" constructor unchanged with `course` and `dateTime`. 

## How to make it more safe and clear

I  


creation, operations, printers

## types of creation

## domain creation

## technical (re)creation

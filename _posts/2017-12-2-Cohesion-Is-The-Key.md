---
title:  "Cohesion is the Key"
author: “keithwillcode”
avatar: "img/authors/keithwillcode.png"
image: "img/cohesion_is_the_key.jpg"
date:   2017-12-2 23:44:12
---

Having high cohesion in your classes is one of the top skills to possess as a software engineer. Let me start with a story before diving in.

When I first started writing code (around age 12/13), my main objective was to get my application running and working. I wanted to see it do something! There is something very special about being so naive about maintainability, architecture and cleanliness that you get drawn into the mindset of producing something that works. I remember being in college and writing an FTP client just for fun. I didn't know the tricks of the trade to make multithreading in a Windows application not look like complete crap. Nor did I realize that making a lot of small classes that do very little would have been extremely beneficial in making sense of the 15,000 lines of code I had written. But, there was something incredible about that. Just sitting on a couch, pounding out code that gave me a working FTP client.

What I realized later is that our code will always have to work. If it doesn't, we won't be able to continue our careers as software engineers. That's when writing clean and maintainable code became another huge priority for me. I've dealt with enough legacy code over the last 10 years working professionally to now realize that taking the time up front to ensure we are making the lives better of the engineers who follow in our footsteps is hugely important. We don't want to be the one who gets cursed for years down the line because our name showed up in a `git blame` command for adding something completely ridiculous that is now causing engineers to lose sleep at night. Or, even worse, handcuffing them into not being able to easily change what we've done without adding a ton of time and risk to the project.

So how do we write maintainable code? Well, there are many aspects to this, but I'll just focus on the 1 thing that has been proven to work time and time again. 

**`Cohesion` is the key!**

Above having the correct data layer in place, above separating concerns of the UI and your domain, even above having a beautifully designed CQRS system that has your read and write stacks separated, make sure you have insanely high cohesion. If you do this, the rest will fall into place.

## What is cohesion?

Cohesion, in the context of classes, is the extent to which a class uses member variables in its methods. If many to all members are used in many to all of the methods in a class, your cohesion is high.

## How do we obtain high cohesion?

When designing a class, where do you start? Some engineers who live and die by TDD will start with a set of tests. Fantastic. Others may start with class diagrams. Ehh. Others will get a specification from their product manager and just start hacking away at the production code because they've been told they only have 2 weeks to complete the feature, which is potentially unreasonable, but they have absolutely no way of altering the deadline. 

No matter where you start, closely watch the member variables in your class. Each method you add, take a moment to look at how many private members it is using. If it's using all of them, that's ideal and amazing. If not, that might be ok, but only as long as methods don't start to only use a small subset of your private members. What we are really trying to avoid by making our cohesion high is having classes that have too many responsibilities. 

A common mistake I see is when engineers think of objects in terms of what I'll call "buckets". They name a class very generally and then convince themselves that a method "belongs" on that object because it relates to that entity in the system. Take, for example, a `User` class. If you build a complex system in which a `User` can have many, many questions asked about it, how can you keep the cohesion of that class high and the number of lines of code low? If you start plopping methods like `GetNumberOfRecentLogIns()` or `GetRecentlyUsedPasswords()` on that class because those concepts "relate to a user", you're doomed. You're going to end up with a class having a bank of methods that use only a couple private members and nothing more. 

A better solution is to be more specific when creating your classes. Let's take that same example. What if, instead of having a method named `GetRecentlyUsedPasswords()`, we create a class named `NewPasswordPolicy` that is instantiated with the most recent passwords used from a data store. Then, we can have a method called `CanUseAsNewPassword(String)` taking the password the user wants to use. The logic for determining whether or not the new password is valid or not is consolidated to this class and this class alone. If we need to change this logic in the future, we don't have to go hunting through a potentially large `User` class. Instead, we'll open this class, see very few lines of code, make our change, run our tests and commit. Done. 

## How do you refactor existing classes?

So what do you do if we are working on a legacy system that has huge classes with poor cohesion? This is actually simpler than you might think but naming the new classes can sometimes be difficult. Start by finding methods that use a small subset of member variables. This will highlight a responsibility living in the class that can be extracted to a new class. If you start on the opposite spectrum just looking for use cases masked as methods, you might run into a larger refactor than you were bargaining for.

Once you've found a method you think you can extract, ask yourself what it's really doing. Think back to the `NewPasswordPolicy`. That class is going to do 1 thing and only 1 thing. Take this same approach when creating and naming your new class. Be specific. 

## Why do this?

Let me bring it back to where I started. It is our responsibilty as software engineers to make features work in the present. True. But, we must be cognizant of the fact that other engineers will follow in our footsteps. If we give them lots of small classes that have just a few variables and very few lines of code, I guarantee they will appreciate us. We have made their lives easier. We have also saved the team and company time and money because our code will be significantly more maintainable.




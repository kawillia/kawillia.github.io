---
title:  "Cohesion is King"
subtitle: ““
author: “keithwillcode”
avatar: "img/authors/keithwillcode.png"
image: "img/noboribetsu.jpg"
date:   2017-10-21 23:44:12
---

When I first started writing code (at age 11), my main objective was to get my application running and working. I wanted to see it do something! There is something very special about being so naive about maintainability, architecture and cleanliness that you just get sucked into the mindset of producing something that works. I remember being in college and writing an FTP client just for fun. I didn't know the tricks of the trade to make multithreading in a Windows application not look like complete crap. Nor did I realize that making a lot of small classes that do very little would have been extremely beneficial to being able to make sense of the 15,000 lines of code I had written. But, there was something incredible about that. Just sitting on a couch, pounding out code that gave me a working FTP client.

What I realized later is that my code will always have to work. If it doesn't, you won't be able to continue your career as a software engineer. So, writing clean and maintainable code became another huge priority for me. I've dealt with enough legacy code over the last 10 years of working professionally to now realize that taking the time up front to ensure you are making the lives better of the engineers who follow in your footsteps is hugely important. You don't want to be the guy or gal who gets cursed for years down the line because your name showed up in a `git blame` command for adding something completely ridiculous that is now causing engineers to lose sleep at night. Or, even worse, handcuffing them into not being able to easily change what you've done without adding a ton of time and risk to the project.

So how do we write maintainable code? Well, other extremely intelligent engineers have written books about this, so I'll just focus on the 1 thing that I do that has been proven to work time and time again. 

Make `cohesion` king!

Above having the correct data layer in place, above separating concerns of the UI and your domain, even above having a beautifully designed CQRS system that has your read and write stacks separated, make sure you have insanely high cohesion. If you do this, the rest will fall into place.

## What is cohesion?

Cohesion, in the context of classes, is the extent to which a class uses member variables in its methods. If many to all members are used in many to all of the methods in a class, your cohesion is high.

## How do we obtain high cohesion?

When designing a class, where do you start? Some people who live and die by TDD will start with a set of tests. Fantastic. Others may start with class diagrams. Ehh. Others will get a specification from their product manager and just start hacking away at the production code because they've been told they only have 2 weeks to complete the feature, which is completely unreasonable, but they have absolutely no way of altering the deadline. 

No matter where you start, closely watch the member variables in your class. Each method you add, take a moment to look at how many private members it is using. If it's using all of them, that's ideal and amazing. If not, that's ok too, but only as long as methods don't start to only use a small subset of your private members. Consider the following example:

PUT EXAMPLE CODE HERE

## How do we refactor existing classes?

This is actually simpler than you might think but naming the new classes that come out of the refactor can sometimes be difficult. The first place to start is to find methods that use a small subset of variables.




---
title: "Building a Crime Tracker Using Chicago Public Data and Google Apps Script"
date: 2017-11-16T13:28:18-06:00
draft: true
---

*Note: the code for this project is available [on github](link).*

This is a quick project-based post showing how to build a crime tracking tool using Google Sheets scripting and the City of Chicago's Open Data APIs. I'm writing this in such a way that inexperienced coders can follow along and experienced coders (hopefully) won't get bored. Also, I should mention that the specific instructions for accessing Chicago's Open Data applies only to Chicago, so if you live elsewhere, sorry! Maybe your city has some publicly available data of its own -- if not, write to your city officials! Open public data has [done a lot for Chicago](link).

## What are we going to build? ##

What we'll be building is a crime tracking email listhost, which sends out weekly emails to subscribers with a list of the crimes that happened in the previous week near specific addresses in the city. That sounds like a lot, but Google Sheets and Chicago's publicly available crime data will make it easy for us. 

Originally, I built this for the public school that I work at to help us be aware of serious crimes that may have affected our students, but [other uses -- safe path checker?]

## Before We Start: What's an API? ##
*Know all about APIs? Awesome! [Skip ahead.](#step 1)*

XXX Shorten and rework analogy -- need something re method of transmission. In sandwich shop, 'piece of paper' doesn't match to anything -- telephone call?

I mentioned the acronym API, which may be confusing if you haven't heard of it before. It doesn't need to be confusing -- an API is really just *a standardized way to ask a computer for things*. For example, in this blog post, we'll be asking the City of Chicago's Open Data website for, well, data. We'll ask the Open Data website for the data we want using the Chicago Open Data API. (We'll also be using the US Census Geocoding API and the Google Email API. So your knowledge of APIs is going to come in quite handy!)

Ok, so an API is a way of asking a computer for things. But how do you use an API? Easy. Here's an example:

Imagine you're at a sandwich shop. Normally, you'd look at the menu, decide what you want, and then tell the person behind the counter: 
```
I'd like a Turkey sandwich with mayo and no onions.
``` 

But imagine that the person behind the counter is very, very literal. (Like a computer.) If you don't ask for your sandwich the exact right way, he won't understand you. He tells you that the exact right way to ask for your sandwich is to write this sentence down on a piece of paper and give it to him:
```
sandwich=turkey&mayo=true&onions=false
```

You give him the piece of paper with the sentence on it, he takes it to the kitchen, and after a minute or two, your sandwich comes out of the kitchen and he hands it to you. Ta-da! You've just done almost exactly what we're about to do with the Chicago Open Data API -- you've *asked for something in a standardized way*. 

It's important to understant that not all APIs follow the same structure: they can look like anything. For example, you could have asked for your sandwich like this:
```
{
  "sandwichType": "turkey",
  "condiments": {
    "mayo": true,
    "onions": false
  }
}
```
or this:
```
sandwichShop.orderTurkeySandwich(mayo="no", onions="yes")
```
You get the idea -- the important thing is that there's a *standard* way to ask for the sandwich.

When we ask for data from the Chicago Open Data API, the way we're going to do it is by creating a webpage URL. Asking the person behind the counter for a sandwich using a URL would look something like this:
```
https://www.sandwich-shop.com/order?sandwich=turkey&mayo=true&onions=false
```
Notice the question mark ```?```, which separates the 'normal' part of the URL (```https://www.sandwich-shop.com/order```) and the part where we're asking for our sandwich (```sandwich=turkey&mayo=true&onions=false```).


[1] Curious what API stands for? It's [Application Programming Interface](https://en.wikipedia.org/wiki/Application_programming_interface), which is a lot, but it makes sense if you think of the person behind the counter as the "Interface" through which you talk to the kitchen, which would make you the "Application" (ie, customer) that wants to use the data (ie, the sandwich) for "Programming" (ie, eating).

## Step 1: Set up our Google Spreadsheet ##

## Step 2: Using Google Apps Script on our spreadsheet ##

## Step 3: Accessing the Chicago Crime API ##

## Step 4: Accessing the US Census Geocoding API ##

## Step 5: Distance Calculation: Finding Out Which Crimes Happened Near Our Subscribers ##

## Step 5: Send some emails with the Google Email API ##

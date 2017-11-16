---
title: "Does Pandas have a bad API? An excuse to think about API design"
date: 2017-11-16T13:28:18-06:00
draft: false
---
For the past few months, I've been using python's excellent pandas library to do data manipulation for my job. (Mostly involving creating reports from Chicago Public Schools' messy data sources, but more on that a different time.) 

I'm far from an expert with pandas -- actually, I feel like I've only barely gotten the hang of it. If using pandas was like baking, then I'm the guy who can make an apple pie from memory because I've done it a few times, but tell me to bake a cake or a pastry or anything I'm unfamiliar with and I'll constantly check the recipe, make a simple mistake like accidentally put in a tablespoon of salt instead of a teaspoon, bake a terrible cake, and have to try again a few times to really get it right. Which is another way of saying that I feel like I know how to use parts of pandas, but I can't really say that I *understand* pandas.

And, I hate to say it, but it's been a few months and I *still* don't understand pandas. Like baking the same apple pie recipe over and over, I've memorized how to do the things that work, but I can't seem to explain why they work, or apply my knowledge to different parts of pandas. 

For example, if you asked me "Hey Michael, can you reorder the columns in this dataframe," I would say "yeah I got you, here's how":
```python
df = df[[
  "Column1",
  "Column2",
  "Column3"
```
If you asked me to explain *why* that worked, I'd have a harder time. "Well," I'd start, "you're creating a copy of the dataframe ... and you're choosing the column names, like a dict in vanilla python." But then, there's that pesky fact that you're selecting the columns in a dataframe using a two-dimensional list -- what does that mean? What happens when you try to use a one-dimensional list? Is this when you need to use .loc? Wait, did I do it wrong?

Imagine a world where this was how you reordered column names in a dataframe:
```python
df.reorder_columns(["Column1", "Column2", "Column3"])
```
Now if you know pandas well, I bet this is the point where you'd speak up. *Not only is something like that already* ***in*** *pandas*, you might say, *there are even a few different ways of doing it! You can use* ```reindex```*...*
```python
df.reindex(columns=["Column1", "Column2", "Column3"], copy=False)
```
*Or you can use* ```reindex_axis```*...*
```python
df.reindex_axis(["Column1", "Column2", "Column3"], axis=1, copy=False)
```
*Or you can do what you did in the first example, which isn't so confusing when you understand what's going on.*
```python 
# select certain columns from dataframe and reassign them to label 'df'
cols = ["Column1", "Column2", "Column3"]
df = df[cols] 

# equivalent to
df = df[[
  "Column1",
  "Column2",
  "Column3"
]]
```



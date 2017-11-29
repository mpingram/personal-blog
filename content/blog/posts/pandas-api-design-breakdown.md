---
title: "Does Pandas have a bad API? A thin excuse to think about API design"
date: 2017-11-16T13:28:18-06:00
draft: false
---
For the past few months, I've been using python's excellent pandas library to do data manipulation for my job. (Mostly involving creating reports from Chicago Public Schools' messy data sources, but more on that a different time.) 

I'm far from an expert with pandas: actually, I feel like I've only barely gotten the hang of it. If using pandas was like baking, then I'm someone who can make an apple pie from memory because I've done it a few times, but if you tell me to bake a cake I'll have to constantly check the recipe, I'll probably make a simple mistake and not notice it, bake a terrible cake, and have to try again a few times to really get it right. Which is another way of saying that I feel like I know how to use parts of pandas, but I can't really say that I *understand* pandas. Like baking the same apple pie recipe over and over, I've memorized how to do the things that work, but I can't consistently explain why they work, or apply my knowledge to different parts of pandas. 

And, I hate to say it, but I think the reason that I don't yet understand pandas is due to some bad choices in the library's API. Specifically, an API design that doesn't give me an easy mental model to use, that allows me to figure out other parts of pandas by using one part, and allows me to catch errors by myself without having to memorize what the syntax is for each thing in pandas I need to do. [rw]

### An Example, Please

If you asked me "Hey Michael, can you reorder the columns in this dataframe," I would say "yeah I got you, here's how":
```python
df = df[[
  "Column1",
  "Column2",
  "Column3"
]]
```
But if you asked me to explain *why* that worked, I'd have a harder time. "Well," I'd start, "you're creating a copy of the dataframe ... and you're choosing the column names with a list of strings." But then, there's that pesky fact that you're selecting the columns using two-dimensional list -- what does that mean? Why not a one-dimensional list? Did I even do it right, or did I misremember?

Basically, I don't have a mental model for what pandas is doing here; I've memorized the syntax, but I don't understand how it's working. Which means that it's easy for me to make simple mistakes and not notice them, because I'm relying on rote memorization to make sure everything's right; if I had my mental model of pandas in place, I'd understand immediately why a one-dimensional array, for example, doesn't work. [And I'm not saying that having a mental model of pandas is impossible! In fact, after writing and researching this blog post, I 'get' how this syntax works. My point is just that building a mental model of how pandas works is harder than it needs to be.]

### Now Hold On A Minute

Now if you know pandas well, this is a point where you might speak up. *Actually, there are a few ways of reordering columns in a dataframe*, you might say, *and they're a little more declarative too, if that helps. You could use* ```reindex```*...*
```python
df.reindex(columns=["Column1", "Column2", "Column3"], copy=False)
```
*Or you can use* ```reindex_axis```*...*
```python
df.reindex_axis(["Column1", "Column2", "Column3"], axis=1, copy=False)
```
*and lastly, your example isn't as confusing when you understand what's going on:*
```python 
# create a list of the column names you want, in order
cols = ["Column1", "Column2", "Column3"]
# select the list of columns from the dataframe 
#   and reassign the selected columns to label 'df'
df = df[cols] 

# equivalent to
df = df[[
  "Column1",
  "Column2",
  "Column3"
]]
```

You'd be 100% right, of course -- all of those methods make sense, once you understand them. But building that understanding is harder than it needs to be.

### So What's Your Alternative?

Just hypothetically, let's imagine this is how you reorder columns in a dataframe:
```python
df.set_column_order(["Col_1", "Col_2", "Col_3"]) # mutates df
new_df = df.with_column_order(["Col_1", "Col_2", "Col_3"]) # copies df
```
or even something like this:
```python
df = df.select_columns(["Column1", "Column2", "Column3"])
```
I'm going to say there are some advantages here: one, it's a little more self-documenting [...]. [there's no hidden confusion about whether or not it operates in place -- 'set something' sounds like it mutates the original object. Maybe there could be a .with_column_order(columns) method for not mutating the original.] [two], and this one is a little more subtle, you don't need to understand pandas' interior workings in order to understand what it's doing. By contrast, think about how much about pandas you need to already know in order to *understand* that the two-dimensional array method effectively copies the dataframe with the columns in the correct order. You need to know how dataframes [select multiple columns from xxx]. [With the the ```reindex``` and ```reindex_axis``` methods, you have to know and understand what an index is, and that column names in a dataframe are also considered indices, and with the ```reindex``` method you also have to know that `axis=1` indicates that the method should operate on the columns and not the rows, and that the ```axis``` keyword argument silently defaults to 0, meaning rows.

[other pandas inconsistencies?]


[...]
Conclusion: pandas is awful and never use it?

Heck no. You can pry pandas from my cold, dead hands when I'm done with it. I need it.

Conclusion: APIs are bad if they aren't easy to learn and vice versa?

Not necessarily. Sometimes, the natural complexity of the problem the API is solving means that making the API as simple as possible actually makes it harder to use. (See [Basic, Visual.](link))

Conclusion: 

[...]
For criticizing pandas, I've picked a very small hill to die on.


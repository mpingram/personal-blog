---
title: "Pro Tip: Make a Class for Pandas Dataframe Column Names"
date: 2017-12-07T10:30:17-06:00
draft: true
---
When I was learning to use [pandas](https://pandas.pydata.org/), one of my biggest slowdowns was constantly checking that I'd spelled the column names of my dataframes correctly. Situations like this were all too common:

```python3
import pandas as pd

# $ cat person_data.csv
# > PersonNameFirst,PersonNameLast,PersonOccupation
#   Sylvia,Plath,Poet
#   Emily,Dickinson,Poet

df = pd.DataFrame.from_csv("./person_data.csv")

# actual column name is "PersonNameFirst"
df.sort_values("PersonFirstName", axis=1, inplace=True)

# > Traceback (most recent call last):
# <3 million lines of error output...>
# ObjectHashTable.get_item (pandas/_libs/hashtable.c:20477)
# KeyError: 'PersonFirstName' 
```

In order to avoid making that kind of mistake, I was opening Excel while coding to copy/paste the column names from my source data, which required me to constantly switch windows. (Not to mention open Excel, which feels a little bit like visiting my parents.)

I've found a nice little way around this problem, though. I like to declare my column names as enums at the top of my file:

```python3
from enum import Enum
import pandas as pd

class Cols(object):
    FName="PersonNameFirst"
    LName="PersonNameLast"
    Occupation="PersonOccupation"
    Tel="PersonPhoneNumber"
    Addr="PersonStreetAddressFull"

df = pd.DataFrame.from_csv("./person_data.csv")

# actual column name doesn't matter
f.sort_values(Cols.LName, axis=1, inplace=True)
```

This helps for a lot of reasons. First off, now if you misspell a column name, the python interpreter itself will catch it, instead of pandas throwing an error -- you don't have to wait for the code to run, and you don't have to parse another non-obvious pandas error message. (Love ya, pandas!) Second off, and this is why I really like it, you don't need to check Excel for the right column names. If your editor has autocompletion, even better -- you can sit back and let it do the work for you.


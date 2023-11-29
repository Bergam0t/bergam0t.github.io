---
layout: single
title:  "Getting details about UK postcodes in Python"
date:   2023-11-29 15:08:01 +0100
categories: python api snippet postcode
---

In my line of work, I often found myself needing data about UK postcodes. 

[postcodes.io](https://postcodes.io/) is a brilliant site for getting a wealth of information very quickly. 

If you have a large number of postcodes in a dataframe that you want to look up, it's easy to use something like `my_df['postcode_column'].tolist()` and pass it into the code below as your `postcode_list`.

```python
# Import library for making request to API
import requests
import pandas as pd

postcode_list = [
    "SW1W 0NY", "PO16 7GZ", 
    "GU16 7HF", "L1 8JQ", 
    "EX27JW" # example missing space
    ]

# Send API request, passing in your postcodes as a list
postcode_lookup = requests.post(
    "https://api.postcodes.io/postcodes", 
     json={"postcodes": postcode_list}
)

# Check the response. 200 is good! 400 is bad.  
postcode_lookup.status_code

# Convert into a dataframe
postcode_df = pd.json_normalize(
     postcode_lookup.json()['result'],
     sep='_'
     )
```



This will then output a rather nice dataframe you can subset and join into your main dataframe using something like

```python
my_df_with_lookup = my_df.merge(
    postcode_df, 
    left_on="postcode_column", 
    right_on="query", 
    how="left"
    )
```

Enjoy!

p.s. 

The code below is an alternative way to do the conversion step that will give you slightly nicer column names.

Note that you'll lose the original query, though, which is a pain if you are trying to join back, as the 'postcode' 
column here will have a normalised/formatted postcode instead, which may not be what you passed in!

``` python
postcode_df_alt = pd.json_normalize(
    [postcode_result['result'] 
     for postcode_result 
     in postcode_lookup.json()['result']],
     sep='_'
     )
```

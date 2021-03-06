---
templateKey: blog-post
related_post_label: Check out this related post
tags: [python]
twitter_announcement: I just dropped a new post check it out.
path: 3-things-to-automate-with-python
title: Three things to Automate with Python
date: 2020-06-01T05:00:00.000+00:00
status: published
description: Here are three things that I see my non programming counterparts doing every single day.  These really sum up so much of what folks do within an office.
related_post_body: ''
related_post: []
cover: "/static/3-things-to-automate-with-python.png"
twitter_cover: ''
twitter_week_1: ''
twitter_week_2: ''
twitter_month_1: ''
twitter_month_3: ''
short_url: ''
devto-url: ''
devto-id: ''

---

Here are three things that I see my non programming counterparts doing every single day.  These really sum up so much of what folks do within an office.  So many of us dabble in or become power users of spreadsheets without knowing there is an alternative out there that can save us time, automate boring things, and allow us to open up our minds for the part that we add value, Thinking about the data.  Lets face it, stitching together spreadsheets is zero value add by itself, but if you can see something in the data and take action on it, this can be huge value add to your company.


## Merge a directory full of spreadsheets into one

I see this one all the time.  One team gets a spreadsheet from another team once per month and they need to stich all the pieces together.  Excel really opens the door for some nasty hidden bugs in your manually stiched together data.  It also takes time out of your day that you dont need to spend.

``` python
import pandas as pd
from pathlib import Path

csvs = Path.glob('raw/*.csv')
csvs_combined = pd.concat(csvs)
csvs_combined.to_csv('processed/combined.csv')
```

## Fetch data from a url

It might be possible that the other team shares their data on a website.  If you can get access to the data via a url, as in the example below there is no need to go to the website to save the data every week/month, you can have python do that for you.  It's very likely that you will need to combine this with step one in many workflows.  Now your data compiling can be done in one single running of a script.  Your data is still in a format that excel can read and you can stick with a hybrid workflow while you become comfortable in python.

There is no shame in opening excel to do something in 5 minutes that would take an hour of research to do in python.  If you stick to it though, piece by piece everything will come together.  You will be able to do more in python than you could imagine in excel and you will wonder how you did it without the help of python.

``` python
import pandas as pd

cars_url = 'https://www.kaggle.com/abineshkumark/carsdata/download/xrvGk4JtQZJZetxwsCCy%2Fversions%2Fl2HR9tTLKz8MzHMAjBcl%2Ffiles%2Fcars.csv?datasetVersionNumber=1'
cars = pd.read_csv(cars_url)

cars.to_csv('cars.csv')
```

## Fetch data from a database

This one can be a bit trickier, often requires hunting down tables that are undocumented. Getting access, and figuring out the crednetials.  If you can get over that hump though it is likely that you will have access to several data source that you typically use in one place.  From there you can learn how to join them together to create powerful workflows.

SQL can be a very daunting language to learn but if you spend an hour with it you will know enough to at least get the data into python or excel.  You can continue to hone your sql skills and move more of your aggregation/analysis into the database for better performance.  If you are asking for 1M rows for a 10 row report the efficiency gains of doing that aggregation in the database and not sending 1M rows over the wire can be immense.

``` python
import pandas as pd
from sqlalchemy import create engine

engine = create_engine('postgresql://scott:tiger@localhost:5432/mydatabase')

sql = 'select * from inventory'

with engine.connect() as connection:
    inventory = pd.read_sql(sql, con)
engine.dispose()

inventory.to_csv('cars')
```

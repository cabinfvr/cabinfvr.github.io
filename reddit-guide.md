# 💫 A Quick Guide to The Reddit API

Are you confused about the Reddit API? This is guide is going to be focused on the Reddit python library, `praw`, and how to use it, get your credentials, etc.

## Getting Started

### Create the application

To view all the apps that you have authorized and created, head to the [reddit prefrences](https://www.reddit.com/prefs/apps) and create an application.

Fill in the info.
![](https://ace.kxd.fm/$YG6KgpCFslNLtdtSIkSCzA.png)

Then, select `script` from
- web app
- installed script
- <mark>script</mark>

and tada! You've created a Reddit application! 🎉
Now, let's get those credentials.

### Obtaining Credentials

So here's how to obtain your credentials. After you've created your bot, here's where the credentials are (it can be pretty scary at first.)

![](https://ace.kxd.fm/$I-CsYnw2YwqcxNC_ejhAQQ.png)

So, in this case, my secret would be `Vd9Y20SC4wXOADREYl_B7NZbYrNoXA`, and my ID would be `HnyhhBUeszHSV5Oiol7PSQ`. (Don't worrry- I've deleted the bot, invalidating the credentials.)

## Basic Programs

To start with some basic programs, go ahead and open a terminal/shell program and run `pip install praw`. This will install a python library that's made for handling the reddit API.

Do you want to scrape a subreddit for random titles, perhaps r/showerthoughts?

Well, you can do so using PRAW (Python Reddit API Wrapper). So go ahead and plug this into your favorite text editor:

```python
import praw

reddit = praw.Reddit(client_id='clientid',
                     client_secret='secret',
                     user_agent='cabinfvr')
```
So, just replace the credentials with yours. The `user_agent`, can literally be anything. Maybe it's `cabinfvr`, or `cabinfvr/1.0`, or something like that. If you want to imitate a web browser (which wouldn't help- but okay.)

Here's some web browsers:

```
Chrome - Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36
Safari - Mozilla/5.0 (Macintosh; Intel Mac OS X 13_4) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/16.5 Safari/605.1.15
Firefox - Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/114.0
Opera/GX - Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36 OPR/99.0.0.0
```

And now that's all good and said, let's scrape the web.

### Grabbing random posts from a subreddit

So say you want to grab a random post from a subreddit.

Here's a quick program to do that:

```python
import praw
import random
import os

reddit = praw.Reddit(client_id=os.environ['CLIENT_ID'],
                     client_secret=os.environ['CLIENT_SECRET'],
                     user_agent='ShowerThoughtsFetcher/1.0')

subreddit = reddit.subreddit('showerthoughts')

posts = list(subreddit.random_rising(limit=50))
random.shuffle(posts)

non_nsfw_posts = [post for post in posts if not post.over_18]

def get_post():
  return random.choice(non_nsfw_posts).title
```

It return's a random posts title. How it works, is:
- `non_nsfw_posts` checks if its not labeled as `over_18` 
- `reddit.subreddit` checks the subreddit you want.

Here's another program:

```python
import praw
import random
import requests

reddit = praw.Reddit(
    client_id="YOUR_CLIENT_ID",
    client_secret="YOUR_CLIENT_SECRET",
    user_agent="YOUR_USER_AGENT",
)

subreddit = reddit.subreddit("anarchychess")
random_posts = subreddit.random_rising(limit=5)

for post in random_posts:
    print("Title:", post.title)
    print("Description:", post.selftext)
    
    if post.url.endswith(('.jpg', '.jpeg', '.png', '.gif')):
        response = requests.get(post.url, stream=True)
        if response.status_code == 200:
            with open("image.jpg", "wb") as f:
                f.write(response.content)
            print("Image saved successfully.")
        else:
            print("Failed to fetch image.")

    print("---------------------------------------")

```

---
part of cabin's guides. learn more at [cabinfvr](https://cabinfvr.github.io)

![]([https://ace.kxd.fm/$4-_rX1AcyO1p8XTTcNO03A.png](https://ace.kxd.fm/$ZXX6L7OdwofV9RDdTEU_1w.png))

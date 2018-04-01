---
layout: post
title:  "Fumbling Through Twitch Authentication"
date:   2017-11-15 21:40:00 -0500
categories: python, testing
---
Prior to stepping into learning MEAN stack and taking a few extra front end specific online courses, I had been playing around with setting up sanity tests for the Twitch.tv API. Tonight I wanted to circle back around to it again and see what I could get done with it.

Fist thing I did was head to the documentation... only to find that everything had changed... again. They're calling this their big update that they're moving towards from here on out, with things being more "streamlined" and "professional". First impression is that they're removing a lot of metadata and requiring even more API calls. I guess that's why they bumped their API request limit up from 1/sec to 2/sec.

After finding a bug with their documentation page (small screen sizes hide site navigation...), I finally got the info I needed to actually start testing the API. For someone like me whose just trying to learn, I feel like their documenation enters the overload category. As I'm just trying to hit their API, I needed to use the [OAuth Client Credentials Flow](https://dev.twitch.tv/docs/authentication#oauth-client-credentials-flow-app-access-tokens) method that they outline on their page. Filling in my data and sending a post returned the needed token.

This token then needs to be included in all of the request messages that gets sent to the API. In my playing around, everything else returned a 401 response. Python's request library makes this easy. ALl that needed to be done was to create a simple header and include it with any of the requests that I made:

{% highlight python %}
headers = {'Authorization': 'Bearer '+token}

In [24]: basic.requests.get('https://api.twitch.tv/helix/games?id=493057', headers=headers).json()
Out[24]:
{'data': [{'box_art_url': 'https://static-cdn.jtvnw.net/ttv-boxart/PLAYERUNKNOWN%27S%20BATTLEGROUNDS-{width}x{height}.jpg',
   'id': '493057',
   'name': "PLAYERUNKNOWN'S BATTLEGROUNDS"}]}
{% endhighlight %}

And that got me up and running to start making my API requests
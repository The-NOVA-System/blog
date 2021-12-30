---
title: App Mockup and UI
excerpt: progress update on the app with some ui mockups
author: Garv Shah
---
{% include header.html %}

# Yay, App Design!
So continuing from the last blog post, I've been working on the app over the holidays. Even though I didn't exactly get 
as much done as I wanted to, I have a UI mockup that I'm pretty proud of so far. The app is based on the wireframe below from [here](https://www.uplabs.com/posts/crypto-app-6a473389-202b-4cee-ad23-94cf46c172cd). <br> <br>
![wireframe]({{ site.baseurl }}{% link static/wireframe.png %}) <br>
Using some ~open source github repos~ (which are always useful), I have a little non-functional demo ready: <br>
<video muted autoplay controls width="100%"> <source src="{{ site.baseurl }}{% link static/mockup.mp4 %}" type="video/mp4"> </video>
Being programmed in Flutter, the same app showcased as a MacOS application here will target the web, iOS, Android and the Windows store.
It is mainly designed as a mobile app, so there may be some usability issues when it comes to that, but it seems to be working pretty well so far.

# Next Steps:
The next steps should be pretty straight forward, as I've decided which API I want to use and just have to hook it up now.
The one thing I'm worried about is that Nomics may not offer graph data in the exact way I want it, so creating a "detailed"
view for each crypto may prove a tiny bit difficult. I'd rather not use one API for the graphs and another for the data, which
would kind of be a mess. I've asked a few people for feedback on the UI so far, and what I've got is:

* add the time period next to the crypto name (one day, one week, etc)
* add up or down arrows to green/red values on side
* remove brackets from value (can signify negative)

<br>
The main feedback has been the time period not being clear enough, so I'll just integrate a default into settings which should solve that. 
Besides hooking it into the API, adding a login system with Firebase should be pretty easy. The main use for the account system in the app is 
just currency conversions from fiat to fiat (the one stored in the database will most likely be USD, while people here in Australia will 
probably use USD) as well as the leaderboards. Overall, progress is going well!

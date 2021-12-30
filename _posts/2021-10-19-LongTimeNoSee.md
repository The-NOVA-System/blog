---
title: Long Time no See
excerpt: an update on progress
author: Garv Shah
---
{% include header.html %}

# It's been a while
woah. It's really been a while since I last wrote a blog post. The last time I wrote, I had *just* integrated an icons api, hadn't I?
That feels like ages ago... Well, even though I haven't been writing much, that doesn't mean I've stopped working on the app. In fact, 
I've made a whole lot of progress, which I'll hopefully be able to summarise without going on for too long!<br>

# Graphs suck man
Y'know how I said I thought I got the graphs working asynchronously? Well that was far from perfect. I don't exactly remember much anymore 
but all I remember is that these graphs were being a severe pain. Essentially what would happen is that the graphs would load once with no data in them 
and then once again from the api, which was messing with things and making the graphs render weirdly:

<video muted autoplay controls width="100%"> <source src="{{ site.baseurl }}{% link static/mockup_5.mp4 %}" type="video/mp4"> </video>

From what I remember, clearing the graph data wasn't exactly simple. What happened is I got the data loading from Nomics just for Bitcoin, 
but the problem is, it would load inconsistently. 

Dark Mode Screenshot                                                             |  Light Mode Screenshot
:-------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------:
![screenshot]({{ site.baseurl }}{% link static/dark_semi_working_charts.png %})  |  ![screenshot]({{ site.baseurl }}{% link static/light_semi_working_charts.png %})

As shown above, it would load for some of them, but not for all of them. The worst part about it is that it wasn't at all, and it would just only load 
half of the time. No matter what I tried to do with the other graphs, they would just be empty. Eventually, I figured out this was because of Nomics' one second limit 
on their free plan. What I was doing was sending my requests, and it would reply with "hey slow down" but I'd try to parse that string as a graph and it would be empty. 
I tried fixing this for a bit, but as evident by this screenshot, that didn't go so well:

![text conversation]({{ site.baseurl }}{% link static/angry_text.png %})

Me saying I went backwards referred to the fact that I thought I had solved the problem from the video, but after I tried fixing the 
problem from the screenshots, I had actually lost progress (somehow). Finally, after a lot of frustration, I slept on it. This 
proved to be very effective, because the next morning I found a way to use Flutter's FutureBuilder to load the api call first, and then (and only then) 
render the graph widget. That resulted in a working graph integration for one cryptocurrency (still had to separate them).

Dark Mode Screenshot                                                        |  Light Mode Screenshot
:--------------------------------------------------------------------------:|:----------------------------------------------------------------------------:
![screenshot]({{ site.baseurl }}{% link static/dark_working_charts.png %})  |  ![screenshot]({{ site.baseurl }}{% link static/light_working_charts.png %})

# The icons API actually wasn't so great
Sooooo, the whole last blog post was about integrating an icons api right? The one that I said was really really good and that I wish all APIs were like? 
Well, it turns out it has some limitations, which resulted in me getting rid of it completely (so much for all that time I spent on it :P). The issue is, 
and I have no clue why this happens, but sometimes their API just goes down on Heroku, and is up in a few hours. The project hasn't been touched by them in 3 years, 
so I don't understand why, but that's the case. The disappointing discovery was that this is basically the case 50% of the time, and even when I started self-hosting, 
my bad wifi speeds meant that it wasn't great (plus I don't want a dependency that I have to manage). The solution I had implemented for a while was that it first fetches 
the coloured API for an icon, and if that doesn't return something, then it fetches Nomics for the icon. The problem with this is, it actually has to wait for a response 
from the icons API first, which means icon loading takes longer than it necessarily has to. This combined with the fact that it doesn't support many icons at all led to me 
deciding to phase it out. 

# Microsoft Store Submission
ALSO, I submitted the app to the microsoft store for review! It took them about 4 days to get back to me, but they sent this back: 

![screenshot]({{ site.baseurl }}{% link static/microsoft_submission.png %})

It's a bit unfortunate, but I see where they're coming from, because I said that the app educates, but at this point it doesn't do that 
in any way shape or form. We'll probably just have to wait until later, when the app actually has the features it says it has to create 
a valid submission. Either way, if we can't get the app on the Microsoft store, we can always just have it as a website by itself!

# Full API Integration
After I finished making the graphs all load from one source, the next task was to make them all load from different sources. This also proved 
relatively difficult, but I don't exactly remember the precise issues I had with implementing this feature. All I remember is quite a few issues with 
the one second rule that Nomics has. I got it working by using the sparkline endpoint instead of the exchange history endpoint, and integrating that 
into my charts class. Works pretty well, and I was really happy once it was done! Screenshots:

Dark Mode Screenshot                                             |  Light Mode Screenshot
:---------------------------------------------------------------:|:-----------------------------------------------------------------:
![screenshot]({{ site.baseurl }}{% link static/dark_api.png %})  |  ![screenshot]({{ site.baseurl }}{% link static/light_api.png %})

<video muted autoplay controls width="100%"> <source src="{{ site.baseurl }}{% link static/api_integrated.mp4 %}" type="video/mp4"> </video>

The loading times shown in the video were significantly improved on through some ~nifty~ optimisations, but really what I wanted was lazy loading.

# Lazy Loading
Lazy loading, otherwise known as infinite pagination, is when you can keep scrolling infinitely, and you never reach the end. It's like what YouTube does 
with their videos, where the feed never ends! This is apposed to normal pagination, which what google does, where you reach the end of the page and you
have to click to go to the next page. The latter is extremely easy to implement (it only took me like an hour), but lazy loading proved to be a lot more difficult.
The first problem was that I had written my code terribllyyy. My whole app was one big listview, and then my widget was a listview inside a listview (a bad idea I've learned), 
which meant that my project hierarchy stopped me from being able to access the position of the scrolling. In other words, because of the way Flutter works, I was unable to tell if 
you had reached the bottom, which is a pretty important part of lazy loading. The solution to this was pretty complicated, and involved the use of slivers. All scrollviews in flutter are made of slivers
(a listview is a type of scrollview), and they are basically very custom versions of a normal scrollview. Setting them up is a bit complicated, but it means you 
can fine tune them to do exactly what you want, how you want. Scrollviews and listviews are great, because most of the time they do what you want and don't require much setup, 
but in this case, a sliver was needed. They really intimidated me at first, but I eventually figured it out, and in [this](https://github.com/The-NOVA-System/nova_app/commit/541e4734f7e064d5ce49d3dbe366e14ef8f73eae) 
commit, I managed to fully redo my structure so that the app worked like intended. This had some other positive side effects, those being that pull to refresh actually worked now (i had 
implemented it before, but since it couldn't tell where the position was, it was just never called), and since it was actually programmed properly now, the widget listview could dynamically 
load and unload widgets when they were on screen to save computational power. This was a bit of an issue before, because when you switched tabs, the whole app froze for about 2 seconds, but now, since 
widgets have started being loaded dynamically, it's much less of an issue.

## Appending to the ListView Builder
So, even though I got the app coded how it should have been in the first place, actually appending to the bottom of the ListView builder was much harder than I expected. 
It was pretty easy to detect when you were at the bottom, but adding to a listview isn't too simple. Honestly, I was pretty stuck, and every solution that I tried 
ended up failing for one reason or another. Listview builders don't have a native append method, and the only array they come from is the future of the api call, which 
would have required me to create a stream. I tried a lot of things and a lot of things ended up failing. I eventually slept on it, and had a semi working solution. What it was 
a nested listview builder (one inside another), where the outer one increased in size by a counter, and the inner one was my normal listview. Whenever the normal listview loaded, it would increment
the page counter, so the next should have theoretically been on the next page. The problem was, it had a weird issue where instead of loading the next page, it loaded the exact same page again. 
I thought this may have been because I was incrementing the page counter and that wasn't rendering properly, so instead I made it so I was modifying the future by extending it. 
For some reason, it still did the exact same thing. The more I messed with it, the weirder it got, where if I just swapped their order, somehow the "previous list" value was the future, but then if I did one of them 
by themselves it worked fine and AHHHHH. It made me go crazy, cause it didn't make any sense at all. It still doesn't make sense. The behaviour was fully unpredictable, which I disliked very much. 
Somewhere along the way, I realised I didn't even need the outer listview builder anymore, so I decided to remove it. And then it decided to work?! I don't know why, but that arbitrary change fixed it, and I'll take it!
Suffice to say, infinite pagination/lazy loading works now, and it works wonderfully, so you can keep scrolling forever and always keep getting results :D

# Summary
There's a lot that I've done over the past week, and didn't even mention any of the bug fixes that I've gone through. The API is officially fully implemented 
so the next steps are as follows:
1. Create a login system with firebase
2. Create a "detailed" menu where you can select the timeframe of the information
3. Make it so you can purchase cryptos with the system

As always, up-to-date builds can be found [here](https://nightly.link/The-NOVA-System/nova_app/workflows/flutter/main). Note that the MacOS version just fully doesn't work as of now, but that should be all fixed when 
releasing the app. Have a good day!

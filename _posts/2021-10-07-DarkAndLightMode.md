---
title: Dark and Light Mode
excerpt: why does theming cause so many issues ?!?
author: Garv Shah
---
{% include header.html %}

# Today's Headache
Today's headache came from theming issues, woo! So essentially, I wanted to implement a simple dark/light mode toggle. 
I already had both the themes set out, so it should be pretty easy right? If only it were that simple... <br>
There's a pretty good [flutter package](https://pub.dev/packages/adaptive_theme) that supposedly made the job pretty easy. 
I could have just used the built in theme and dark theme (which defaults to light and changes by the system theme), but I wanted 
to have a settings page that would make this a bit better, so I opted for the package. It was easy enough to set up, but then 
I witnessed the bug you can see in the video below: <br>
<video muted autoplay controls width="100%"> <source src="{{ site.baseurl }}{% link static/mockup_2.mp4 %}" type="video/mp4"> </video> <br>

It was really annoying, and honestly, I don't believe it was entirely my fault, mostly just the way the google_charts 
package I was using was coded. This resulted in everything updating, but the charts breaking and giving me the error

```
Failed assertion: line 120 pos 12: '_drawAreaBoundsOutdated == false': is not true.
```

I searched the error up, and the only solution I could find was [this](https://github.com/flutter/flutter/issues/31778#issuecomment-593146310). 
Frankly, it works, and I was able to implement it too. The only problem is , when you switch to a different tab and then switch back, it stays 
on loading forever, and just never changes. I have no clue why it does that, but after about 6 hours of work, I gave up trying to make it work 
the way I intended. <br>
<video muted autoplay controls width="100%"> <source src="{{ site.baseurl }}{% link static/mockup_3.mp4 %}" type="video/mp4"> </video>

# The Dodgy Solution:
So in the end, the solution I'm working on is pretty damn dodgy all things considered. Since it breaks the graphs if they're 
on screen, but they work fine again if the page is switched, I just created a new settings page where you can't see the graphs 
at all. This way, you change the theme, go back and it looks normal. Honestly not the most ideal solution, but it works for 
now and it's not the main functionality of the app anyways. It was a pretty big waste of time to be honest, but at least we 
got some theming done in the end :(

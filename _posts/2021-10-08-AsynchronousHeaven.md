---
title: Asynchronous Heaven
excerpt: yayy, theming actually works now!
author: Garv Shah
---
{% include header.html %}

# Programming is so fun when it works :D
So, after being relentlessly annoyed by how annoying computers were, I spent a majority of today working on the app, 
a lot of it during class time, but that's fine since I finished all my other school work anyways. Anyways, the time and effort from 
today paved the path for genuinely working theming (yayy!!) <br>
As I mentioned in the last post, I came across a solution that I managed to implement, but wasn't working particularly well 
for me. What the solution suggested was to make the loading of the charts asynchronous, something which frustratingly, 
google charts doesn't seem to offer within the package itself. I *did* say I gave up on this idea yesterday, but while in 
bed, I realised that this issue wouldn't end here. Cause if the charts fail to load asynchronously, they won't be able to load
data from the api at all (it'd just give me the same error)! >:( <br>
Remember when I said this?

>but it works for now and it's **not the main functionality of the app anyways**

Yeah, well I was wrong. Loading from the API 100% is the main functionality of the app, and I didn't want to have the same 
headache then as well. Sleeping me also realised that the bug caused by switching screens probably unloads the charts and
sets it back to the loading widget, but it never reloads the widget since the setState function isn't called. 
Therefore, all I had to do was get back to where I was (probs should have uploaded to GitHub, more on that later), and somehow 
force that setState function to call whenever I switch pages. Woo!

# But most of the time it doesn't work :(
Well, I *was* right, in that the setState function was never being called, this much was true. The problem arose when I actually 
tried to call the setState function. My first idea was to just move setState into a void function outside the scope of the widget, 
and call it whenever I needed to load the chart. Unfortunately, Dart is nothing like Python, and actually requires you to have the
variables initialised in the function scope (who woulda thought). Soo, instead I fiddled around for a bit too long working out how to 
force setState to happen. Eventually, I did what I should have done in the first place and analysed the if statement, which goes something
like this: 

```Dart
if(!Config.isLoaded()) {
  Config.loadChartDataList().then((value) =>
      setState(() {
        //do stuff })
      }
  );
};
```

The if statement is checking whether the Config._loaded value is true or not, and if it's false, then only will it load
the rest of the chart. This moment was a breakthrough, and with just a little bit of fiddling, I got it to run like this: <br>
<video muted autoplay controls width="100%"> <source src="{{ site.baseurl }}{% link static/mockup_4.mp4 %}" type="video/mp4"> </video>

As you can see, the theme toggling works perfectly, and you can switch from screen to screen pretty easily. I did spend the next 
few hours trying to implement a pull to refresh feature, but the widget for the wallets is non-scrollable, due to the fact 
that its parent is scrollable, so if it was you wouldn't be able to go down. Therefore, the RefreshIndicator has to go on the 
parent widget, which is the root of the whole application, but if the onRefresh function is called there, it's outside the scope 
of the whole widget tree and therefore updating Config._loaded does change its value, but doesn't trigger the rest of the tree to 
refresh. This time for real, it's not essential functionality, and though it's probably possible with slivers or the like, it's 
a bit too much effort for me right now (I should probably focus on the important functionality first). Besides that, I also added 
null safety support to the app which is neat, and the app should be your system theme by default!

# GitHub
Going through this, I realise that I probably should have started uploading the code to a GitHub repo from the beginning, so I don't 
lose my code and have an archive of what it was before. So, after probably a bit too long, it's all uploaded! You can access a pre-release 
version of the app [here](https://github.com/The-NOVA-System/nova_app/releases/tag/mockup). Currently, I've only compiled MacOS and Android 
binaries, but that should be enough for now. woop woop

## Update
I added a workflow that automatically build and uploads artifacts every time I commit to GitHub no effort on my side. So if you want *pre-*pre-releases, go to the following link and click on your relevant operating system

### [download link](https://nightly.link/The-NOVA-System/nova_app/workflows/flutter/main)

# Summary
After much effort, we've finally finished the mockup phase of the app! We've got some very good groundwork laid for the future, 
and hopefully this can be done within 2 weeks or so, it will definitely be fun to use once it all is. Thanks for reading :))

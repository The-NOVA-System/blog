---
title: App Store Submission (yay!)
excerpt: i really need to start writing more blog posts
author: Garv Shah
---
{% include header.html %}

# It's been a while (again)
It's one of those rare times again that I write a blog post (woo)! At first, it was because I took a break from the project for 
like a week, and then it was because I hadn't done enough work, and then small things started pilling up and I had done enough work, 
but I would write a blog post laterrrr, and before I know it, I've essentially finished the app and haven't written anything in a month lmao.<br>
No, but seriously, there's been a lot of progress, much of which I haven't covered in the slightest, so get some popcorn ready, cause this is gonna be a lot >:)

# Login System/Firebase
So one of the first things that I worked on after the last post was a login system. I spent quite some time designing a mockup
(thank you open source github repos), and I ended up with this:

MacOS Screenshot                                                                     |  iOS Simulator Recording
:-----------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------:
![login screenshot]({{ site.baseurl }}{% link static/macos_login_screenshot.png %})  |  <video muted autoplay controls width="100%"> <source src="{{ site.baseurl }}{% link static/ios_login_sim.mp4 %}" type="video/mp4"> </video>

Honestly, I believe that the design above looks a lot better than what we ended up with, but the problem was that it just wasn't dynamic enough, and with 
all the different screen sizes we intended to support (along with the difference between login and signup), it ended up not looking great. This coupled with 
the fact that we had to remove the google and facebook buttons (as per mr heinrich's request), made it look a bit clunky, so I switched to a more minimal system 
which works well with firebase:

![final login]({{ site.baseurl }}{% link static/final_login.png %})

It *does* look a lot more simple, but honestly it works better, and the login system will be redesigned eventually anyways, since once the 
beta testing is over, I'm going to open it to the public instead of just out school. Besides that, the login system is really cool, and links 
the app to our firebase database which is where all the transactions happen!

# Small things make a whole
Over the course of these few weeks, there's been a lot of small things that I've fixed that have added up to make the app a bit more than a small bit better.

### Dropdown Menu
For example, there's a little dropdown menu to select a timeframe for the data. The graphs don't update yet, but that's because the graphs in a smaller timeframe 
kind of look crap with the Nomics API. Their sparkline endpoint became depreciated while I was using it, and the other historical crypto data has become 
part of the paid plan, which means that no matter what, charts taken from Nomics won't really look *the best*. Eventually, I wanna shift to some other chart provider, 
which isn't great because it means I have **another** dependency, but it's better than having less than ideal graphs.

### Leaderboards
Another "small" thing is the leaderboards, which are a cool addition. Originally, I was using a bucket sort for the values, but that screwed up with decimals and which multiple duplicates, 
so I ended up realising I could just use Dart's built-in sort method which was cool. I also made the profile pictures load from [here](https://avatars.dicebear.com), 
which is a really cool API that generates unique default profile pictures so that everyone is special!

![leaderboard]({{ site.baseurl }}{% link static/leaderboard.png %})

### Password Reset System
Self-explanatory ngl

### CORS Proxy
Finally, besides a few more formatting changes to make the app look a bit better, I made a CORS proxy, which was an attempt to bypass some school Wi-Fi blockages (I had permission don't worry). 
Basically, I realised that the icons wouldn't load on the web due to CORS (godamn it, it's always CORS isn't it), and the people at Nomics (who had previously given me CORS Passthrough for the normal API) 
said that they wouldn't be able to give me passthrough for the AWS assets, advising me to use a CORS Proxy instead. I did as they said, and it worked well for a while, until I realised that 
the school blocked almost all CORS proxies I could find online (sadge). This resulted in me talking to Mr Heinrich and Mr McCarthy (see email below) about what could be done to fix this, and Mr McCarthy said 
I could just build my own!

![CORS Screenshot]({{ site.baseurl }}{% link static/cors_ss.png %})

So, needless to say, I did, and you can view it [here](https://corsproxy.garvshah.workers.dev) :D<br>
It's not exactly ideal since I'm on the cloudflare workers' free plan, which means that if a lot of people start using the app then the icons will stop loading, but it's fine for now. 
I plan to stop supporting the websit eventually anyways, since it's so buggy :P <br>
On that note: Linux and Windows builds don't work anymore, since FlutterFire doesn't support either of the platforms, which is a shame. Hopefully that gets fixed eventually. 
I'm keenly keeping my eyes on (this)[https://github.com/invertase/flutterfire_desktop] repo, which may be an eventual desktop implementation, which'd be great.

# Buy/Sell System

Wallets (Sell) Screen                                                 |  Buy Screen
:--------------------------------------------------------------------:|:-------------------------------------------------------------------------------:
![login screenshot]({{ site.baseurl }}{% link static/wallets.png %})  |  ![login recording]({{ site.baseurl }}{% link static/buy.png %})

A pretty big thing that was added was the buy/sell system. This is basically the final building block in making the minimum viable version of the app, 
and minimum it definitely is. Currently, there are no transaction fees, you can only purchase using USD, and there are no withdrawal at all. Really, I just made 
it as quick as possible to get it out there, since it's better to have a working version on the app store with updates pushed afterwards than to have nothing at all. 
Also, when we started beta testing, a couple of dupe glitches were discovered, which were fun to fix. 
I'm definitely going to work on this later (hopefully before the workshops, which were confirmed to be during the end of year program btw), and it'll be improved once the app is on 
the app store. Speaking of which:

# App Store Submission!!!
Sooo, we've got an app store submission! Apple was being a bit slow on the email game, and they didn't reply to me very quickly, so even though I could've gotten 
the one free year of apple dev through my Apple Scholarship, it was better to get the submission done soon, so we just bought it. I've been going through the process 
of submitting and reviewing and so forth, and I'm still waiting to get it on the store. The following is a screenshot of the rejected Mac app for the app store:

![screenshot]({{ site.baseurl }}{% link static/mac_deny.png %})

Besides that, it's been pretty cool using TestFlight to beta test the app, and we've gotten quite a few people on the app just testing stuff out. 
Here's a link to join the beta (note that you gotta have a cgs email to make an account):
<br><br>
[https://testflight.apple.com/join/RrZvlZS9](https://testflight.apple.com/join/RrZvlZS9)
<br><br>
I've also got continuous delivery set up with the iOS app, and we have a pretty active userbase of friends who are just helping us 
iron out bugs before we release :D

# Summary
The app is nearly done, and a lot of it will just be polishing it out with little features here and there that make using the app a more pleasant experience. 
Honestly, we're pretty close to the workshops, which means the end of this project at least in an official manner, so I most likely won't get all of these implemented 
ever, but it's nice to have them listed if I ever do get back to it:
1. Just a little bug where you can scroll on the app bar, should be an easy fix
2. Improving the buy/sell system to make it more realistic with the ability to trade any crypto with fees
3. An improved login system with providers like google or github, apple sign in would be cool too
4. Natsuki's suggestion: badges for beta testers and developers and stuff
5. A buy me a coffee section in the about page
6. A search function to filter through the cryptos
7. A detailed view on profiles to be able to see what assets they have
8. Improved graphs that actually change their timeframe and don't look trash (probably not with Nomics)
9. The ability to change your profile picture
10. Adding a few easter-eggs for fun
11. Windows and Linux Apps

As you can see, the list is pretty long, so hopefully it's more like a checklist for whenever I get to it :D
<br>
Thanks for reading. Have a good day!

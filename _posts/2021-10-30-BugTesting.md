---
title: Bug Testing and Firebase Discussion
excerpt: Polishing up
author: Liam Shaw
---
{% include header.html %}

# Polishing up our app, and using Firebase
With the app in its final stages of development, we decided to dedicate this week to bug testing and patching any problems that might occur. Initially, this all occurred on the web version of the app, as both the testflight iOS beta version and the iOS app store version were both still under review. With the help of some friends who we invited onto the app, we managed to immediately find and patch a few duplication glitches that occurred in the buying and selling menus.
<br>
<br>
We quickly found that entering a value of 0 or a negative wreaked havoc through the system, giving users their inputted money back or allowing them to have as much money as they want. Fortunately, two simple lines of code containing inequality equations and an error message were able to prohibit people from exploiting our system.
<br>
<br>
The testflight beta of the app came out towards the end of this week. To our great excitement, our app worked flawlessly, with much better loading times in comparison to the web version of the app. It seemed so smooth and responsive! This gave us some very high expectations for the final app, which is soon to appear on the app store.
<br>
<br>
Fortunately, since we host all our accounts on Google’s Firebase system, we were able to quickly reset any accounts who used the exploits while bug testing. Firebase has proved to be incredibly useful, and I’m glad we ended up choosing it over alternatives. We spent a while discussing what the best service to use was, and ended up choosing Firebase for its simple interface and free hosting, and ability to push updates to certain groups of people (for example, our beta testers with accounts using the @caulfieldgs domain). 
<br>
<br>
Eventually, the hope for our app is to migrate the large majority of the interface to being hosted on Firebase, so that we can push live updates and not have to wait for them to be reviewed as updates through the app store. Hopefully, this will provide a better user experience over all.

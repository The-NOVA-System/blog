---
title: Icons, Icons, and Colours
excerpt: starting api integration and icons!
author: Garv Shah
---
{% include header.html %}

# The problem with Nomics
As I mentioned in a previous blog post, the api of choice for this project is Nomics. So, today was the day when I decided 
I would start integrating the api into the app! Saying this, I found a problem pretty quickly, and that being that the 
sample data I had included something Nomics did not: colour information. So that I could render my graphs in a matching colour, 
my sample data included Material Palette equivalents of the colours of the logos. My first idea was to get the crypto logo (which 
Nomics thankfully did provide) and get an average colour to plug into the chart. I tried this for a bit, but the charts not working 
the best with async code made this a tiny bit difficult. <br>

# I wish all APIs were like this
So, after a tiny bit of searching, I found a [really cool api](https://cryptoicons.org) that lets you not only fetch the 
crypto logo, but also specify *any* hex colour code so that the logo can be in *any* colour you want. It's honestly pretty cool, 
so what I ended up doing was using this api to fetch the logos, with a random colour from the Material Palette:

```dart
static List matColors = [
    [charts.MaterialPalette.indigo.shadeDefault, "3f51b5"],
    [charts.MaterialPalette.blue.shadeDefault, "2196f3"],
    [charts.MaterialPalette.cyan.shadeDefault, "00bcd4"],
    [charts.MaterialPalette.deepOrange.shadeDefault, "ff5722"],
    [charts.MaterialPalette.green.shadeDefault, "4caf50"],
    [charts.MaterialPalette.lime.shadeDefault, "cddc39"],
    [charts.MaterialPalette.pink.shadeDefault, "e91e63"],
    [charts.MaterialPalette.purple.shadeDefault, "9c27b0"],
    [charts.MaterialPalette.red.shadeDefault, "f44336"],
    [charts.MaterialPalette.teal.shadeDefault, "009688"],
    [charts.MaterialPalette.yellow.shadeDefault, "ffeb3b"],
  ];
```

So essentially, it picks a random entry from that array above, and then uses the corresponding hex value for the api call, and the 
Material Palette value for the charts, etc. It's a pretty neat system (which caches the images too), so now the logos + chart colours will 
always be consistent. 

# Summary
Today was a bit of a derail from what I intended it to be, but honestly it was a pretty nice success with a very nifty API 
that I wish I'd found sooner. I think that there are 3 steps to fully integrating the APIs:
1. Icons and Chart Colours
2. Chart Information
3. Rest of the Information

Besides that, all I'll really need to do when it comes to the actual "information" side of the app is adding a detailed 
view for each of the crypto widgets. Progress is going pretty good so far, so hopefully I'll integrate Nomics soon :D <br>
Thanks for reading!

### PS: the builds for [today's commit](https://github.com/The-NOVA-System/nova_app/commit/d3071ccec625df238ad43c9218a3f8b7a965221c) are [here](https://nightly.link/The-NOVA-System/nova_app/workflows/flutter/main) :D
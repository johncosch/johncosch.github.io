---
layout: default
title: Z-Wave of the Future
---

## Z-Wave of the Future
I apologize that it's been so long since my last post. I guess 2016 hasn't really thrown me any curveballs that I've felt I had to write about yet. Well, until yesterday that is. I've been helping to organize the technology for the Stamford Hackathon recently. This basically means working with the founder to make sure people have cool s*** to hack on (vendor & sponsor API's/ SDK's), and that they have enough information about how to use that cool s***, to build their own cool s*** over the weekend. Yesterday, some awesome engineers from the hackathon's main sponsor, [FlowThings](https://flowthings.io/), came up to Stamford with their entire IOT arsenal of sensors who's data will be available through the FlowThings platform during the hackathon. Tom, their CTO, explained to me that most of the sensors they brought communicate through a protocol called Z-Wave. But what was this Z-wave word these guys were throwing around like beads at Mardi Gras?  Well... it was the first curveball of 2016.

![z-wave](http://www.z-wave.com/assets/logo-4126408fad032d66d512ed2395dbb4856da10ee07cfbd916b587c0e9ae48f9b7.png)

Z-wave is a form of low-latency wireless communication that is able to send small data packets across a mesh network. What this means is that each node, a device that is transmitting a z-wave signal, can utilize other nodes in the network to move data back to the controller. For example, the Flowthings guys set up tons of sensors that contain z-wave transceivers all around the innovation center. As the sensors collect data, they basically act as a team of receivers (no, not football receivers) to send data across large distances back to their controller. The controller which is connected to the internet then passes that data into the Flowthings cloud platform, where you can set filters, callbacks, or add pretty much any kind of logic you might need. Hackathon participants can then hook into the Flowthings platform using their REST or web socket api's to build cool s***.

Z-wave has been around since at least 2008, and other protocols that achieve pretty much the same objective like ZigBee have been around for even longer. So these kinds of mesh networks aren't exactly a bleeding edge advancement, however from what I've heard the Z-wave community has made development much simpler than that of ZigBee. Meaning you don't have to be an electrical engineer to actually get it working the way you want.

I wish I could give you some better insights into the technology, but I just learned about it yesterday myself. I'll absolutely be doing another post on this stuff as I explore the exciting world of mesh networks further. Oh and if your in the Stamford CT area this weekend be sure to sign up for the [Stamford Hackathon](http://stamfordhackathon.org/).

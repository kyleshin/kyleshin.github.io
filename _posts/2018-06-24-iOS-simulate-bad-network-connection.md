---
layout: post
title: "How To Simulate Bad Network Connection To Test iOS Apps"
date: 2018-06-24
author: Kyle Shin
comments: true
---
## How To Simulate Bad Network Connection To Test iOS Apps

When developing iOS applications, it is important to simulate bad network connections.
By testing under such condition, you may be able to catch unintended behaviors
in your app.


To test your app in simulator with bad network connection, you will need to download an Xcode developer tool called Network Link Conditioner. Below is an quick instruction:

1) Open Xcode. Select Xcode -> Open Developer Tool -> More Developer Tools

![path](/images/blog/2018-06-24/1.png)

2) Download Additional Tools for Xcode 9.3.dmg (or whichever version that matches your Xcode version).


<image src="/images/blog/2018-06-24/2.png" width = "65%"></image>

<br>

![path](/images/blog/2018-06-24/3.png)


3) Open the .dmg, and open the Hardware Folder. Find Network Link Conditioner.prefPane and drag it to the Mac System Preferences

![path](/images/blog/2018-06-24/4.png)


![path](/images/blog/2018-06-24/6.png)


4) Open the Network Link Conditioner and you can select various network speed. Flip the switch ON, and now you can test your app in the simulate with your selected network speed. Note that this speed reduction effects your entire computer.


<image src="/images/blog/2018-06-24/5.png" width = "65%">
</image>

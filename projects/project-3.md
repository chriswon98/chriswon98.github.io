---
layout: project
type: project
image: images/smartlogo.png
title: Smart Cubby
permalink: projects/cotton
# All dates must be YYYY-MM-DD format!
date: 2017-12-13
labels:
  - Arduino
  - MIT App Inventor
  - Android
summary: A smart cubby and Android app system designed to improve organization of school life.
---

<img class="ui image" src="../images/cubby.jpg">

Smart Cubby is a custom-made cubby with an Arduino Uno microcontroller paired with a custom Android app also called "Smart Cubby". The Smart Cubby was constructed from plastic and had a total of 10 compartments, one of which housed the Arduino Uno microcontroller. The five larger slots were used for textbooks and the four smaller slots for other items (i.e. calculator). Each of the compartments had an LED light. These would turn on to indicate what items you needed for the school day. An RFID reader and kept track of what was in each compartment by scanning the RFID sticker tags on each item. The Android app allowed the user to input their schedule and related school supplies. This would then connect with the Arduino Uno via Bluetooth and tell which compartments to light up.

I was responsible for developing the Android application using [MIT App Inventor](https://appinventor.mit.edu/). This was done on the suggestion of our professor as I had less than half-a-year of programming experience. MIT App Inventor was design by the Massachusetts Institute of Technology and simplified Android app design by providing code blocks. I used these code blocks to program the interface and the Bluetooth exchange of the user's calendar data. This was initially difficulty because it wasn't the same as writing the code directly. It was more of an understanding of how the functions worked and how to manipulate them for our purpose.

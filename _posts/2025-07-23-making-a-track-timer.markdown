---
layout: post
title:  "Making a track timer"
date:   2025-07-23
description: "I learned a lot during this project."
project: "Track Timer"
---
# First Steps
I did well in my electrical and computer engineering class, and I have soldered before, but there was a lot of steps to go from the idea to a finished project. The first step was simply knowing what parts to buy. I outlined these parts in the project post, which is linked above or in the project tab. After getting a shopping list, the total price for this project was roughly $90, well within my budget.

I love Arduinos, they make this sort of project much more affordable. I found out they made Arduino Nanos with USB Type-C, so I bought 2 of them. Connecting everything to the breadboard was mostly accomplished by watching videos of people using similar hardware, and using random wiring diagrams I could find. 

While researching the nRF24L01 wireless module, I heard many people having reliability issues, mostly due to power problems. I used a breakout adapter with an onboard 3.3V regulator, as well as a 10μF capacitor soldered between the power and ground. I had no issues with reliability, and thankfully getting the modules to communicate was pretty painless.

Three libraries need to be included:
```cpp
#include <SPI.h>
#include <nRF24L01.h>
#include <RF24.h>
```
The pins need to be defined, as well as the address, which can be anything as long as its the same on both:
```cpp
RF24 radio(9, 10);
const byte address[6] = "TIMER"
```
The setup block needs a few things to get the radio started:
```cpp
void setup(){
    Serial.begin(152000);
    radio.begin();
    radio.openWritingPipe(address);
    radio.startListening();
}
```
Once the radio is setup and listening, sending a message is fairly straightforward. Within the loop block, we need to check if there is a radio signal available. If there is, you can read the message with radio.read(). This could be anything, but in the end I went with a long as my data type. I first assembled and tested this, sending the message "GO", and sometimes the receiver would not get the message. I figured a fix for this would be to repeatedly send the current time for a brief moment, so if any message is lost, the receiver can simply start at whatever time was received. Receiving the message looks like the following:

```cpp
if (radio.available()){
    unsigned long receivedTime = 0;
    radio.read(&receivedTime, sizeof(receivedTime));
    timer = millis();
}
```

![](/assets/images/breadboard-finish.jpg)
![](/assets/images/breadboard-starter.jpg)

Once I had those breadboard prototypes created, I took them in a shoebox to the track to test and make sure that they work. They worked in close range, so the only limit left to test was the radio modules' capabilities of range. They worked well, so the next step was to solder them to a board and design a case for them. 

Soldering the components to a board was a bit tedious. My soldering station had a pair of helping hands, I'm not sure if I could have done it without them. I indiviually cut and stripped each wire, and soldered the components to the board. Below is the finished boards inside of their cases, which I had to design as well.

![](/assets/images/track-timer-circuit-boards.jpg)

I had experience 3D modeling in Blender, but this wasn't very similar to what I had modeled before. I was used to modeling and rendering cars and lego sets, not so much in precise CAD work. I started with some videos to get an understanding of what parts I would need to model, most importantly an easy way to access the boards. I decided on a sliding box design, so I created a small box to quickly print and test tolerances. The sliding lid actually worked pretty well on the first attempt, So I decided to print a bigger box to get an idea of how the entire box would work. The second box I printed gave me important information, even though it was a failure almost all around. Even though it should be common sense, it taught me to double check all of my tolerances before printing, because I forgot to make the lid thinner than the opening. The lid printed at the exact same height as the opening, which added stress and cracked the box. These two test boxes are pictured below.

![](/assets/images/track-timer-prototype-boxes.jpg)


![](/assets/images/receiver-3dprint.png)
![](/assets/images/sender-3dprint.png)

![](/assets/images/track-timer-finished.jpg)
![](/assets/images/track-timer-lid-open.jpg)


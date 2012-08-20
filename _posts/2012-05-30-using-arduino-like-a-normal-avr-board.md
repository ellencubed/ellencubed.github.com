---
title: Using Arduino as a normal AVR dev board
layout: post
tags: [arduino, avr, avrdude]
catagories: [AVR Dev]
---

So lately I've been moving away from the Arduino's IDE software and getting into coding the AVRs directly. At first I just used
a spare 328p I bought some time ago on breadboard and wired up a power supply. However I started thinking that since I had an 
Uno and Duemilanove that I should just use one of those since I could also make use of the protosheild to make things a bit 
easier. Connecting an AVR programmer and just writing to the 328p wasn't an issue. The problem came about with timing. The Arduino 
is running off a 16MHz external clock and I wanted to switch it back to the 1MHz factory default. 

Fixing this problem just took a quick glance at the datasheet. The default low and high fuse byte values are `0x62` and `0xD9` and 
for the the Arduino's 328p they come set at `0xFF` and `0xDA`. Then I just just connected my USBtiny to the Arduino normal and ran 
avrdude to write the fuse values.

{% highlight bash %}
avrdude -p m328p -c usbtiny -U lfuse:w:0x62:m -U hfuse:w:0xd9:m
{% endhighlight %}

And now it's running off the internal 8MHz clock with the CKDIV8 fuse set which brings it to the factory default of 1MHz. 

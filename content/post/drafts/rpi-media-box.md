+++
author = "Doug Smith"
title = "Raspberry Pi as a Media Player"
date = "2023-11-11"
description = "Squeezing enough power out of an rpi to play media"
toc = true
draft = true

categories = [
  "Projects"
]
tags = [
  "Raspberry Pi"
]
+++

# Intro: My somewhat petty motivations

In the 2020s is a funny decade for the cable box. Like, streaming has given us
access to so much media on the computer that a lot of people give up on that
special converter strapped to the TV. So many people in fact that we have a
phrase for it: "cord-cutting". Meanwhile, the computing power of everything
else attached to your TV, from game consoles to DVD players to even the TV
itself, is massively increasing their computational power. This is usually
to support a variety of internet powered content-delivery features, be it
the aforementioned streaming or some wacky reimagining of smartphone apps,
and the result has broadly been an increase in entertainment options for the
consumer. And I think I don't like it.

Like, all those internet-enabled devices were being critiqued for enforcing
planned obsolescence and experience-ruining DRM before we knew that people
could use them to spy on you. And the UX isn't great. Like, you used to just
hit buttons to configure your TV, which passed through all the images from the
things you plugged into it, which you configured seperately, with or without
the image it displayed on the TV, but now those lines are all blurry. Like, do
you watch Netflix on the TV or through the Xbox connected to your TV? Because 
the controls and performance can be very different, as will the level of ads
thrown at you during a watching session.

Like most device problems, my first instinct to solve it is to throw everything
away and see what can be done with FOSS. The goal is to make a single media box
that collects as much of my media experiences as possible so I can control/configure
them. It's hard to dispense with the Smart TV entirely 
(they don't really make a lot of "dumb" TVs, especially not at the 
higher tier of quality), but if all I'm using is one HDMI port I'm hoping I won't
notice.

# Step 0: Getting an Rpi running

So before building anything, you need to make sure you have a working Raspberry
Pi. There are a lot of tutorials out the for RPi setup, basically you just get
your device, flash the appropriate verion of the Raspbian OS to an SD card,
plug the card into your Pi, and connect a power source. Pretty straightforward,
I can even verify that this will work as a media player by loading youtube on a
browser and playing a video...

And if you're in a similar situation to me, this is the first hurdle. The video
experience for me chugged horribly an the OS threw alerts about "insufficient power
to CPU".

## Verifying Your Power Source

So as it turns out, the Pi3 isnt actually powered by a MicroUSB. Well, it is, the
power port fits a MicroUSB connector ad not much else, my old MicroUSB phone
charger turned the thing on, but it only sort of works, because the Pi demands
more power than a MicroUSB should be able to supply. Per the standard, a MicroUSB
connector can handle 2 Amperes at 5 volts, and the Pi3 needs all of it to drive
its CPU. The problem is, a lot of MicroUSB cables that are for charging other
devices or doing data transfer aren't capable of delivering at that standard,
you need to identify a good power supply out of a field of false promises.

How do know if you have a good cable? Well, if you own a multimeter you can
actually test this yourself. Just configure a meter to the 2A/5V range
expected, arrange the MicroUSB port you want to test so it's facing you,
and touch the live (red) probe to the further left pin while touching the
ground (black) probe anywhere on the outside of the port. The multimeter will
read the voltage the port delivers, which is the power supply you Pi has to
work with. If you're not seeing 5V (I found a lot of my device chargers 
delivered 1.5V, which I guess could be a different standard for data-delivering
cables?), or having trouble getting a reader (the pins can be recessed on 
some ports that make readings hard to get), you can just get a new cable
certified to deiliver power to the MicroUSB max for about $10. I've found
CanaKit works fine.


# Step 1: Running a media player

Now we've got our power source, we're running the CPU at its full power
level, and we can try and load that video... and it still chugs. Maybe its
just the network? Nope, VLC runs a file slowly as well. It's important to
remember that this isn't a particularly powerful computer by modern PC
standards. Just running the stuff you would use on your Linux PC is probably
not going to work when the task is as intensive as audio/video. We need to
optimize for the compute we have.

## Option 1: LibreElec the OS that just barely runs media

The first option to try and run things is to use a packaged project that is
just about made for this purpose. LibreElec is a minimal OS layer packaging
just enough support to launch the media application Kodi.

And I'll say right off, this works. Like, if you load it onto an RPi and play
a file, it'll run just fine. But when I tried to stream media, things got a
little rough. Kodi supports streaming... kind of. Streaming services are
delivered via Kodi-specific add-on applications, but these need to be implemented
for each video source you want to watch from. You might get Netflix, but I
don't know if anyone is working on CuriosityStream. And of course, they have all
the baggage of any open source app interfacing with DRM-controlled centralized
IP. That is to say, they break quite frequently when the service providing
corporations change something, and in some cases that change is dciding to cut
off support for this type of third-party support. Because there isn't a full
graphical environment, you can't switch to a browser either.

So getting that versatile support of web on Kodi will take some work.
Contributing one's own browser is an option (and has been done in the past),
but I want to try to see how some other alternativs work out-of-box.
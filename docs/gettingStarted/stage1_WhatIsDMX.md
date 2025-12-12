---
layout: default
title: Step 1 - What is DMX?
parent: Getting Started
nav_order: 1
---

# Step 1 - What is DMX?

DMX, short for Digital Multiplex, is a communication protocol used in the entertainment industry to control lighting and effects. It allows for the transmission of data from a controller to various lighting fixtures and devices, enabling synchronized control over multiple elements in a lighting setup.

For VRChat, DMX is used to create dynamic and interactive lighting experiences within virtual environments. By utilizing DMX, creators can design intricate lighting setups that respond to user interactions, music, or other in-world events.

## Key Concepts of DMX:

At its core, DMX is a protocol that allows channel data to be passed to parameters on individual lights. The reason why this is sometimes confusing is because there is a lot of jargon obfuscating the actual functionality of the system. So lets get through some of the jargon to make things a little easier.

## Channels, Fixtures, Universes:

A channel is another name for a singular float, it simply is a value from 0 to 1. 8-bit floats such as that in DMX are able to produce values from 0-255, this means that we have 256 possible values to work with. 

A fixture is another name for a lighting fixture, there are many different types of fixtures in the lighting world. Spots, Washes, Movers, Statics, Effects, Bars are a few different types of fixtures. These will all become familiar to you as you progress through your DMX journey. A fixture can have multiple channels to manipulate parameters in real time. An example of this is the 5-Channel fixtures in VRSL. Where they have Intensity, Red, Green, Blue, and Strobe channels. Meaning the fixture takes up 5 channels of data.

A universe of channels is 512 channels. DigitalMultiplex (DMX) can send 512 channels down a single cable, this allows for daisy chaining fixtures, so if you have 100 fixtures, you don't need 100 cables going to each fixture from the console. Only one from the console to the closest and then you can daisy chain around the rest of the 100 fixtures.

![GrandMA3 Light](/assets/images/GrandMA3Light.png)

Modern consoles can do many more than a single universe with GrandMA3 (A lighting software/hardware) allowing for 1024 Universes of data, that is over 500k channels. Of course, it is not practical to have 1024 singular cables running into a console. This is where a technology called Art-Net enters the picture.

## Art-Net

Art-Net is an IP based version of the DMX cables, modern fixtures support either direct Cat-5 input, or Art-Net will be piped to an "Art-Net node" on the stage/backstage to then be distributed via cable, theoretically being limited to 32768 universes, or just under 1.3 million VRSL 13 channel movers.
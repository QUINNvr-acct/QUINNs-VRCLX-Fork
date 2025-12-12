---
layout: default
title: Step 2 - Getting DMX into VRChat
parent: Getting Started
nav_order: 2
---
# Step 2 - Getting DMX into VRChat
In this step, we will guide you through the process of getting DMX data into VRChat using gridnodes and VRSL. First of all though, what is a gridnode?

## What is a Gridnode?
Art-Net as mentioned before is a protocol for sending DMX data over a network. However, VRChat does not natively support Art-Net, so we need a way to convert that Art-Net data into something that VRChat can understand. This is where gridnodes come in. A gridnode converts Art-Net data into a grid of pixels that gets streamed into VRChat as a video feed. Each pixel in the grid corresponds to a DMX channel, allowing VRChat to receive and interpret the DMX data.

![Art-Net GridNode](../assets/images/GridNode.png)

The GridNode is limited to 3 universes in black and white mode, or 9 universes in full RGB. For the sake of this explanation we are going to be using the gridnode in its default, 3 universe mode.

## How do I get a GridNode?
There are a few different options when it comes to choosing a gridnode.

- VRSL GridNode: This gridnode is the original gridnode made by ACChosen, this option is paid, and very simple to use.
- FNode: This gridnode is made by the Furality Team, this option is free and has support for different modes that allow for added complexity.
- HNode: This gridnode is made by HappyRobot33, this option is also free and by far is the most complex, it allows for a plethora of options and configurations, even going beyond DMX data into other professional protocols such as protocols for drone light shows.

## VRSL Shaders

The way that the VRSL shaders work for DMX from the video screen, is that the shader will be told to look at a specific area on the video, and to take the value of that pixel, hence the white and black grid of values.

```glsl
half getValueAtCoordsRaw(uint DMXChannel, sampler2D _Tex)
{
   // DMXChannel = DMXChannel == 15.0 ? DMXChannel + 1 : DMXChannel;
    uint universe = ceil(((int) DMXChannel)/512.0);
    int targetColor = getTargetRGBValue(universe);

    universe-=1;
    DMXChannel = targetColor > 0 ? DMXChannel - (((universe - (universe % 3)) * 512)) - (targetColor * 24) : DMXChannel;


    uint x = DMXChannel % 13; // starts at 1 ends at 13
    x = x == 0.0 ? 13.0 : x;
    half y = DMXChannel / 13.0; // starts at 1 // doubles as sector
    y = frac(y)== 0.00000 ? y - 1 : y;
    
    float2 xyUV = _EnableCompatibilityMode == 1 ? LegacyRead(x-1.0,y) : IndustryRead(x,(y + 1.0));

    float4 uvcoords = float4(xyUV.x, xyUV.y, 0,0);
    float4 c = tex2Dlod(_Tex, uvcoords);
    half value = c.r;
    value = IF(targetColor > 0, c.g, value);
    value = IF(targetColor > 1, c.b, value);
	return value;
}
```
Taken from https://github.com/AcChosen/VR-Stage-Lighting/blob/main/Packages/com.acchosen.vr-stage-lighting/Runtime/Shaders/Shared/VRSL-DMXFunctions.cginc

You don't really need to worry about this at all, but it is a nice to know where the function is kinda thing, and to know how it works should you wish to use it to make other shaders.
---
title: Isometric Orthographic Camera Zoom in Zoom Out in Unity 3D
description: Programming an isometric orthographic camera zoom in zoom out for 3d unity games.
author: Code Mantid
date: 2021-03-15 21:34:00 +0800
categories: [Gamedev, Unity 3D, Isometric]
tags: [isometric games, isometric camera, orthographic camera zoom, isometric camera zoom, unity 3d, unity camera script, getting started]
pin: true
---

If you want to jump to the code [**click here**](#0x02---zoom-code)

## 0x00 - Introduction

In today's scene, almost 31 years after the beginning of the pseudo 3d 90's isometric game fever, developers usually choose this specific style almost for aesthethic purposes only, without knowing beforehand the particularities of this choice.

Developing isometric games have it's own complexities and dealing with it all can easily become an overhead in the beginning, specially when you haven't your own engine toolset yet. 

Most artists don't work with this lack of perspective(orthographic) in a daily basis as well, which creates another hardship to handle. Perspective can easily be an artist's best friend, specially if you need to change the player perception about something and hide map elements. Mistakes tend to become even more visible than normal in isometric art.

Doing isometric games with Unity 3D is a feasible way of creating the initial blueprints without diving in completely from scratch. It'll help you to understand isometric game mechanics, particularities, the kinds of problems that come within this choice and if it's a worthy pick for your unity project or personal engine.

I usually begin with the camera when doing unity projects, because once I'm done it usually takes a long time before
something needs to be changed again.

Make sure we're using the same **unity version(2020.2)** or test if it works with another one.

Enough talking! Let's learn by doing.

## 0x01 - Eyes first: create an isometric orthographic camera

- Create your camera, find it in hierarchy and change it's rotation in the Inspector section transform to **X: 30º, Y: 45º** 
<br>
> GameObject > Camera
<br>
![Camera](/assets/img/posts/Post_1_isometric_orthographic_zoom/Empty_camera_image.png){:class="img-responsive"}

- Set it's tag to MainCamera
> ![Camera](/assets/img/posts/Post_1_isometric_orthographic_zoom/main_camera.png){:class="img-responsive"}

- Now change your camera projection to orthographic. 
> ![Camera](/assets/img/posts/Post_1_isometric_orthographic_zoom/Orthographic_camera.png){:class="img-responsive"}

Creating a terrain now is not a bad idea, since we'll work in zoom in/out right after this.

> GameObject > 3D Object > Terrain

Position your new terrain as you wish and make sure it's on camera's range.

## 0x02 - Zoom code

> ![Camera](/assets/img/posts/Post_1_isometric_orthographic_zoom/add_component.png){:class="img-responsive"}

**Add the code below as a new script component**

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;


//Zoom in zoom out implementation
public class CameraZoom : MonoBehaviour
{
   //Remeber to assign this Camera in the Inspector
    public Camera orthocam;

    /*Positions and dimensions 
    of the Camera view in the Game view*/
    public float m_ViewPositionX, m_ViewPositionY, m_ViewWidth, m_ViewHeight;
    
    /*Should be a const, but letting it this way, 
    so you can choose min/max better using your 
    inspector*/
    [SerializeField]
    public float MAX_ZOOM_SIZE = 20f;

    [SerializeField]
    public float MIN_ZOOM_SIZE = 10f;

    private void Start()
    {
        //proportional camera ratio without black borders with these values
        m_ViewPositionX = 0;
        m_ViewPositionY = 0;
        m_ViewWidth = 1;
        m_ViewHeight = 1;

        /*It enables your camera that is orthographic*/
        orthocam.enabled = true;
        
        //Default distance, before we zoom in/out
        orthocam.orthographicSize = 17f;       
    }
    
    private void Update()
    {  
        //Zoom in/out with mouse scrollwheel till {MAX/MIN}_ZOOM_SIZE is reached
        if(Input.GetAxis("Mouse ScrollWheel") < 0 && orthocam.orthographicSize < MAX_ZOOM_SIZE)
            orthocam.orthographicSize++;
        if(Input.GetAxis("Mouse ScrollWheel") > 0 && orthocam.orthographicSize > MIN_ZOOM_SIZE)
            orthocam.orthographicSize--;
        
        //Set the orthographic Camera Viewport size and position
        orthocam.rect = new Rect(m_ViewPositionX, m_ViewPositionY, m_ViewWidth, m_ViewHeight);
    }
}

```
It's really simple, but the last time I looked around there was no implementations of this, at least for recent versions(with orthographic cams of course).

The next natural step is creating a player with some controls and put our camera to follow him by the map. Work for our next time. 

If there's something I should know or any doubts just ping me somewhere, hope you liked :)

References:
<br>
[Unity 2020.2 Documentation](https://docs.unity3d.com/2020.2/Documentation/ScriptReference/Camera-orthographicSize.html)








SceneKit
===============

## Ambient lighting

Lights in scenekit are supposed to be attached to nodes in every case. This holds true even for directional lights and ambient light.
In the case of the latter, attaching an ambient light to anything but the scene root node has actually no effect. 


## Projecting shadows on a transparent plane

Projecting shadows on a transparent plane needs a little trick. Naively casting shadows on a transparent SCNFloor is not possible, as 
the shadow will not be visible as it's part of the plane and thus will be transparent like the plane. In order to do this, a little trick
consists in creating a white plane with a `.multiply` blend mode and a Lambert lighting model. 

As it's white, any color multiplied by it will remain the same, which means that anything multiplied by the plane's color will appear 
as if the plane was transparent.
With the Lambert lighting model, one can use a directional light to cast the shadows. The directional light will not be taken into account
in the lighting model and will not contribute to the plane's lighting.
This solution actually doesn't impact the shadow rendering mode.

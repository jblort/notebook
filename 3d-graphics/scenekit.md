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

## Soft shadows on iOS

To have soft shadows on iOS, one need to use the `shadowRadius` property, with values in the range [1;3] being acceptable, and the `shadowSampleCount` property set to
an acceptable value. By default it's set to `1` which means that the shadow radius won't have any effect as there's no sampling performed.
Better results are obtained by defining a size for the shadow map as well. The default is `CGSizeZero` which lets SceneKit determines the best one, but it might not 
always work well.


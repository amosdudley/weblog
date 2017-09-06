---
tags: [self-Amos, computation, fabrication, architecture, packing, SLS]
title: "Stochastic Part Packing for 3D Prints"
---
## (Or how to make lots of different stuff, all at once) 
![Hero](https://i.imgur.com/0Ceqegu.jpg)

If the idea of 3D printing hundreds of baseball-sized parts seems daunting, slow, and expensive, you’re probably making two big assumptions: that each part is printed sequentially, and that they are printed with supports. SLS (powder) printing solves the second issue by eliminating the first. 

A person can save time by filling the largest percent of each print layer with parts as possible. Why? Printing objects sequentially is the same as adding Z height to your print, and building on the Z axis of a 3D print is considerably slower than on the X and Y axes. By using a powder-based printer we can print without support material, and nest parts close together vertically and horizontally to give the best possible ratio of part to empty space per layer. This is called 3D part packing. 

We took an unusual approach to 3D part packing for the Fuse Pavilion, which used 144 unique nylon joints 3D printable in a single build volume. Here’s how to pack hundreds of high-detail STL models very quickly with a physics sim and open source software.

## Physically simulating 3D packing

Imagine pouring a bunch of toys into a toy chest. If there are too many toys, the chest will overflow and the lid won’t close… but that doesn’t mean that all the toys couldn’t fit into the chest if they were oriented correctly. 

![toybox](http://i.imgur.com/OGq5dIX.jpg)

This scenario is almost identical to what we can do in Blender! We used Blender’s physics engine to pour parts into a virtual volume, then exploited its collision-avoidance behavior to re-sort them into a tight 3D packing optimized for overlapping concavity.

<iframe src='https://gfycat.com/ifr/AlarmingLawfulAsianconstablebutterfly' frameborder='0' scrolling='no' width='640' height='360' allowfullscreen></iframe>

## Set up the scene:

- Define the print volume boundary by creating five rectangular prisms (four sides and a bottom). Leave the top open, and add a four sided funnel to guide parts into the print volume. Each prism/wall should be a separate object.

- Add Collision and Rigid Body physics modifiers to the walls. Use the “Convex Hull” collision shape (this mode is the fastest and most reliable). Set collision type for the boundary walls to Passive.

- Duplicate your parts to create a set of physics proxy collider objects. These will greatly speed up your simulation. Add a Solidify modifier to expand the collision boundary past the surface of the part. Shell thickness should be set to half the desired minimum distance between parts. 
 
- Add Rigid Body physics to your proxy objects. Set the collision shape to “Mesh”, Sensitivity margin to 1.0, and Friction to 0.0.

- Add a Decimate modifier to the physics proxy objects. This is particularly important if you have high-resolution base models. Parent your base parts to the physics proxy objects by selecting the base, then the proxy, and using [ Ctrl - p ]. 

- Position your proxy objects above the funnel (the high-res parts will move with them).

## Run the simulation:

Now, your parts will fall into the print volume naturally by gravity, and collisions will be determined by simplified proxy objects. See what happens:

- Run the simulation using *[ Alt - a ]*. 

## Compress objects into the volume:

Allowing parts to fall into the volume results in a somewhat loose pack, even though the parts are now nesting together. Let’s compress them further.
 
When objects in the Blender physics engine are forced to intersect, they will fly apart. This behavior is normally annoying, but it’s actually useful in this case - it automatically jitters the pack until there’s no overlap between parts. 

- Create a flat rectangular prism (a “press”) as wide as the opening of your funnel, positioned above your parts. Copy the same physics settings as the boundary walls.

- Keyframe  *[ I ]* the “press” over the course of several seconds from its starting point above the parts, ending with the bottom surface above the top of your print volume. 

- In the Rigid Body Dynamics settings for your proxy models, enable deactivation and add a small amount of damping. This will cause the parts to stop moving once they have found an acceptable position and orientation.

- Run the simulation again.

Instead of simply falling into the volume, the parts are now compressed to the point where they start intersecting. In Blender’s collision model intersection is kind of a ‘high energy’ state, and the parts will wiggle around semi-randomly until they find a ‘lower energy’ state where they don’t intersect. If there is no low-energy position for a part to land, it will simply continue to wiggle. 

## Tips & Tricks:

If your simulation speed is too slow, test out different decimation settings for your proxy objects. 

If you are working with a large number of objects and want to adjust packing settings for all parts at once, simply join all your proxy objects before changing settings, and “separate by loose objects” afterwards.

If objects are clipping through during compression, slow down motion of the press by moving its last keyframe to the right on the timeline. You can also increase simulation Steps per Second and Solver Iterations in Rigid Body Settings.

## Conclusion:

If your parts are simple convex shapes, you will probably get a better packing by simply stacking or arraying them. If you have large concave regions or significant geometric variation between parts, automatic part packing quickly becomes worthwhile. This physics solution isn’t fully automated - it’s a somewhat naive solution that doesn’t detect when your parts are packed or exactly how many can ultimately fit. It is very fast and effective for a certain part packing scenario (ours). I’d love to hear if you test this out for a particular application and find it works better or worse than other methods.

This blog post is a technical follow up about the FUSE Pavilion, <a href="https://formlabs.com/blog/3d-printing-at-scale-fuse-pavilion">a 15-foot installation designed and 3D printed in June 2017</a> with the help of <a href="http://www.aashmangoghari.com"> Aashman Goghari</a>.

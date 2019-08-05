---
tags: [self-Amos, glass art, kiln casting, fabrication, kilncasting, lost-resin, lost-wax]
title: "Casting Glass from 3D Printed Molds"
---
![Hero](https://i.imgur.com/0yUj4rC.jpg)

I had a chance to dip my toes into the wonderful world of glass art, and learn a new way to make things from my friends <a href="http://yoav-reches.com/">Yoav</a>, <a href="http://www.angelathwaites.com/about_my_work.html">Angela</a>, and <a href="https://www.noamandmichal.com/">Noam</a> at the Pilchuck Glass School. We taught the class called “New Footprints in Glass”, using unusual digital techniques to make glass objects. 

Our class was only 8 people, so I wanted to get these techniques to a wider audience! I can’t get over how satisfying glass is. It is surprisingly heavy and cool to the touch, and it’s a hard material which counterintuitively means that it’s easy to polish to a mirror finish. Unlike plastic, it will last **forever.** 

There are a lot of different disciplines and techniques in glass. You’ve probably heard of glass blowing, which is exciting, unpredictable, and a bit performative. I prefer to have more control, and that drew me to *“kilncasting”*. Kilncasting is the opposite of glassblowing: slow, deliberate, and potentially very precise. When you kilncast glass, you make a <a href="https://en.wikipedia.org/wiki/Refractory">refractory</a> mold, place chunks of glass in the mold, and then heat it to about 1500°F, until the glass runs like honey and fills the shape.

If you’re a 3D printing person, and not a glass artist yet, this is something that you can do with access to a glass fusing kiln. As around at your local makerspaces or glass studios. They also just aren’t that <a href="https://www.paragonweb.com/FireFly_Digital.cfm">expensive</a>. Heck, you can even fuse glass in a <a href="https://www.amazon.com/Large-Microwave-Kiln-Glass-Fusing/dp/B012EV9LES">microwave</a>. 

If you’re a fine arts person, you can use basically any 3D printer to make glass art (along with a kiln, same as above). Again, makerspaces or university fab labs are your friend. You definitely don’t need digital skills to cast glass, but they open a lot of new doors in terms of form, texture, and precision. 

*Note:* *This isn’t going to be a kilncasting tutorial - you can find very good instructions <a href="https://www.bullseyeglass.com/images/stories/bullseye/PDF/TipSheets/tipsheet_08.pdf">online</a>.*

I think the most useful thing I can talk about is a few ways to make forms, and how to turn them into molds. 

![Prime slab](https://i.imgur.com/214q06y.jpg)

## 2.5D Reliefs

If you are planning to do some work at home, or in an open studio, reliefs let you to make casting forms without any “burnout”. Burnout is exactly what it sounds like - in some casting methods, you burn (or melt) the positive out of the mold. People who are running glass fusing kilns (in makerspaces, at home, or commercial settings) usually don’t have enough ventilation for plastic burnout. Reliefs are a great way to make glass forms without fumigating the building.

With some clever design design you can create a positive that can be pulled off of the plaster mold away from the positive without causing any damage. Let’s look at how this is done:

**Eliminating undercuts**

*Note: I’m assuming some level of digital fluency here, but you don’t need to be an advanced 3D modeler. You’ll need to know how import models into Blender, and navigate the basic interface.* 

You can use any method of making digital 3D models here. Our students at Pilchuck used 3D scanning, which is a great way to make 3D forms from found objects, nature, or even traditionally sculpted shapes. No expensive equipment required, you can use a camera and some <a href="https://www.3dbeginners.com/list-of-free-photogrammetry-software/">nifty software</a> to capture 3D models. 

Once you have a model, the problem you need to solve is how to make a model with no undercuts, which will break when you go to remove the 3D printed positive:

*Source: <a href="https://www.instructables.com/lesson/Introduction-to-Mold-Making-Casting/">Instructables Tutorial</a> on moldmaking.*

99% of shapes are not set up to have no undercuts. However, **all** shapes can be turned into a relief, by digitally “projecting” the shape onto a surface. We need to make a “depth map”, which is an image that encodes depth. Pure white will be the highest spot in the relief, pure black will be the lowest, with shades of grey all the heights in between.


Left to right: Original model, Depth Map, and 3D printable relief.

A depth map is a great way to eliminate undercuts, because it cannot encode anything that’s hidden from view from a given perspective. As it turns out, anything that is hidden is an undercut.

In case you don’t know how to make a depth map, here’s a Blender project that does this automatically - all you need is a 3D model, and this will convert it to a 3D printable slab with an embossed relief.

Instructions will appear when you open it. Note, this only works with Blender 2.79. Should look like this:



Making the Prime Slab


Here’s a few detail shots of the moldmaking and casting process. I wanted a very smooth surface, so I used a Form 2 (resin) printer. Any layer lines in the print end up transferring through to the glass, which makes polishing a lot more difficult.


To create the refractory mold surface, I poured plaster silica into a temporary mold box. The positive is absolutely glistening with silicone mold release.


I added four walls around the plaster brick with a wrap of ceramic paper, to contain the molten glass during casting. A slab of billet glass was simply placed on top of the open mold, and allowed to melt onto it.


Prime slab, Amos Dudley, 2018

Lost-resin glass casting

I suspect you might not be satisfied only making reliefs. With lost-resin casting, you have much more freedom in what you create - virtually any shape is possible. So what’s the catch? Lost-resin is a casting process that involves a plastic burnout stage. This can only be done with great kiln ventilation, like a big fume hood or by rolling your kiln outside. 

You’ll need a kiln that can reach ~750°C to burn out the resin from the mold. This can double as your glass fusing kiln, although the mold will need to fully cool before you can load it with glass.

Silica refractory molds are extremely fragile, so we needed to print the parts hollow with very thin (~0.7 mm) walls. Otherwise, the force of the expanding resin will break the mold as you burn off the positive. If you’re using FDM 3D printed positives (ie. PLA plastic), this is less important - but the less infill you can get away with the better. 


Some modeling clay forms a “feed cone” that is scooped out before burning the pattern. We use string to create thin channels for air to escape — this helps prevent air from getting trapped by the molten glass as it flows through the mold.


After burnout, soda-lime glass is placed into the feed cone and the molds are set into the kiln to be cast. Over the next three days, gravity and heat do the rest of the work. Make sure to place these molds in sand - they can break in casting, and the sand will protect the bottom of the kiln.


Some stanford bunnies. More techno-kitsch than art, but I like them anyway.


Negative Space Inversions

A beautiful aspect of glass is that you can embed visible forms inside other shapes! This is really easy to do with digital design and kilncasting.

Take two shapes and overlay them in CAD so that they partially overlap. There needs to be a large and robust connection from the inner shape to the outer shape.
Subtract the inner object from the outer.
3D print positive, use lost-resin investment casting as above.
High polish the outside of the casting. The inside remains frosted and visible.
(Optional): Fill the hollow inner void with some colored resin.



Negative-space snake. Or negative space-snake? Amos Dudley, 2018

One of our students, Iole Alessandrini, used a combination of the three techniques to make this piece, which I thought was pretty cool. She started (in classic architectural fashion) by crumpling a piece of paper.

Then she 3D scanned it, extracted 2.5D projection of the surface, and pulled the edges downwards to make a solid volume. For the matching piece, she subtracted this volume from a similar shape. 

Iole Alessandrini, 2018. 3D scan of crumpled paper, turned into nesting three dimensional volumes.



Let me know in the comments if you give this a shot! I’m happy to go into more detail about anything I’ve glossed over. 


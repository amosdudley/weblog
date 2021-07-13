---
tags: [self-Amos, reprap, ECM, electrochemistry, electroplating]
title: "Machining Steel with 3D Printed Plastic"
---
## Experiments in Sinker ECM
![ecmCAD](https://i.imgur.com/asmgMvv.png)
*Schematic of ECM testbed*

**ECM Wiki**

## From Gun Barrels to Cookie Cutters

Electrochemical machining (ECM) is an unusual way of machining hard metals. If you're familiar with electroplating, it's like that, but in reverse. Instead of adding metal to the surface of an object with electricity, you remove metal in a controlled way. ECM is used to cut tiny parts very accurately (micromachining), bore holes with very large aspect ratios, and create complex surfaces in hard metals.

ECM has some very interesting advantages compared to "mechanical" machining, which I think would be underexploited in the maker world, if it were possible to ECM metals at a small scale:

- Zero tool wear. The tool doesn't come in contact with the workpiece, it simply advances towards the metal while chemically eroding material away at the same rate.
- No tool marks or burrs.
- No large forces on the workpiece or the tool, which makes it possible to machine very delicate structures.
- ECM is virtually silent (the only noise is produced by a few pumps).
- No heat affected zone, and no heat-treating equipment required for annealing / rehardening.
- Theoretically high accuracy (though, we'll get to that later).

ECM is scarcely seen outside of industrial settings, so don't feel bad if you haven't heard of it. It's a technology that seems to have gotten stuck in the 1950s. Part of the reason for that is, making ECM tools has always been challenging and expensive. The ECM tools themselves have to be conventionally machined out of metal (usually conductive copper), and work kind of like sinker E**D**M, in that they have the inverse shape to the part you want to cut.

<a href="https://i.imgur.com/RgAL5J7.png"><img src="https://i.imgur.com/RgAL5J7.png" height="300" title="source: imgur.com"/></a>

*Diagram by Okuwobi et al.*

The big difference is that an ECM tool needs to inject pressurized electrolytic fluid, right at the interface between the tool and the workpiece. The electrolyte is the chemical transfer medium that provokes metal ions to cleave off the metal stock, and also flushes the unwanted particles (which quickly form a thick sludge) away at high speed.

From what I can tell, controlling the fluid behavior of the electrolyte through tool design (where the conduits go, etc.) is the main reason ECM is expensive, because there's an unavoidable amount of trial and error involved.

![plants-crave](https://i.imgur.com/fkzxFaT.gif)

So an ECM tool is not really trivial to make. Or hasn't been. But, it's rather easy to make arbitrary 3D shapes with a 3D printer, and copper happens to be the easiest metal that one can use to plate over plastic parts (with one of the least toxic plating baths). Combine those two things, I thought, and maybe you can take most of the expense out of the tool making step. Maybe, just maybe, it would be possible to electrochemically machine steel stuff in the enforced quietude of my apartment.

I imagined a process where a positive 3D printed "tool" is plated with a very thin layer of metal. Then, these tools could be used in a way similar to sinker EDM, to machine complex net shapes with resin-print-like tolerances, in tough metals like pre-hardened steels.

I embarked on this foolhardy journey with only the foggiest understanding of chemistry and electricity. Armed with an SLA printer, a sacrificial RepRap, some plating chemicals, and a general idea of how to use them, I forged into the unknown.  

## Build Overview

Ok, not totally unknown. In the past year or two, intrepid souls on the internet have taken it on themselves to use the principles of ECM to cut gun barrel rifling at home. Whether or not you think the end product is worthwhile, the process seems to work. If these folks can cut helical groves in (hopefully) barrel-grade steel with what amounts to a wire wrapped plastic churro and some salt water, maybe it's not that big a stretch to expect some kind of results with a metallized 3D print that's attached to the Z stage of a RepRap.    

<a href="https://i.imgur.com/WGS2In8.png"><img src="https://i.imgur.com/EghvbqZ.png" height="700" title="source: imgur.com"/></a>

## Electroplating Resin

Depending on the plate thickness, it can have a relatively negligible impact on the overall dimensions of the part.

<a href="https://i.imgur.com/WGS2In8.png"><img src="https://i.imgur.com/WGS2In8.png" height="700" title="source: imgur.com"/></a>

## Designing a Tool
<a href="https://i.imgur.com/3vxXUz3.jpg"><img src="https://i.imgur.com/3vxXUz3.jpg" height="700" title="source: imgur.com"/></a>

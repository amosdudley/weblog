---
tags: [self-Amos, reprap, ECM, electrochemistry, electroplating]
title: "Machining Steel with 3D Printed Plastic"
---
## Experiments in Sinker ECM
![ecmCAD](https://i.imgur.com/auGRB7k.png)
*Schematic of ECM testbed*


## The Design

**In this post:** I wanted to find out whether electroplated SLA resin parts could be used for sinker ECM.

Electrochemical machining (ECM) is an unusual way of machining hard metals. If you're familiar with electroplating, it's like that but in reverse. Instead of adding metal to the surface of an object with electricity, you remove metal in a controlled way. ECM is used to cut tiny parts very accurately (micromachining), bore holes with very large aspect ratios, and create complex surfaces in hard metals.

ECM has some very interesting advantages compared to "mechanical" machining, which I think would be underexploited in the maker world, if it were possible to ECM metals at a small scale:

- Zero tool wear. The tool doesn't come in contact with the workpiece, it simply advances towards the metal while chemically eroding material away at the same rate.
- No tool marks or burrs.
- No large forces on the workpiece or the tool, which makes it possible to machine very delicate structures.
- ECM is virtually silent (the only noise is produced by a few pumps).
- No heat affected zone, and no heat-treating equipment required for annealing / rehardening.
- Theoretically high accuracy (though, we'll get to that later).

If you haven't heard of ECM, you're in the majority. ECM is uncommon outside of industrial settings (think machining turbine blades), because making the ECM tool is challenging and expensive. ECM tools are themselves conventionally machined out of copper or other soft conductors, and work kind of like sinker EDM, in that they have the inverse shape to the part you want to cut.

The big difference is that an ECM tool needs to inject pressurized electrolytic fluid, right at the interface between the tool and the workpiece. This fluid is the chemical transfer medium that provokes metal ions to come off the metal stock, and also flushes the unwanted particles (which quickly form a thick sludge) away at high speed.

Copper also happens to be one of the easiest metals to plate over plastic parts (with one of the least toxic plating baths).

I imagined a process where a positive 3D printed "tool" is plated with a very thin layer of metal. Then, these tools could be used in a way similar to Ram E**D**M, to machine complex net shapes with resin-print-like tolerances, in tough metals like pre-hardened steels.

<a href="https://i.imgur.com/RgAL5J7.png"><img src="https://i.imgur.com/RgAL5J7.png" height="300" title="source: imgur.com"/></a>

*Diagram by Okuwobi et al.*

## Build Overview
<a href="https://i.imgur.com/WGS2In8.png"><img src="https://i.imgur.com/EghvbqZ.png" height="700" title="source: imgur.com"/></a>

## Electroplating Resin

Depending on the plate thickness, it can have a relatively negligible impact on the overall dimensions of the part.

<a href="https://i.imgur.com/WGS2In8.png"><img src="https://i.imgur.com/WGS2In8.png" height="700" title="source: imgur.com"/></a>

## Designing a Tool
<a href="https://i.imgur.com/3vxXUz3.jpg"><img src="https://i.imgur.com/3vxXUz3.jpg" height="700" title="source: imgur.com"/></a>

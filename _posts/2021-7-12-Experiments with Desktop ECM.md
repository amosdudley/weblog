---
tags: [self-Amos, reprap, ECM, electrochemistry, electroplating]
title: "Cutting Steel with (Electroplated) Plastic"
---
## Experiments in Sinker ECM
![ecmCAD](https://i.imgur.com/asmgMvv.png)

*Schematic of ECM testbed - first machining results at the end of the page*

**Writing in progress... divert your eyes.**

## Cookie Cutters and Rubber Stamps

Electrochemical machining (ECM) is an unusual way of machining hard metals. If you're familiar with electroplating, it's like that, but in reverse. Instead of adding metal to the surface of an object, you remove it in a controlled manner. ECM is used to cut tiny parts very accurately (micromachining), bore holes with very large aspect ratios, and create complex surfaces in hard metals.

ECM has some very interesting advantages compared to "mechanical" machining, which I think would be underexploited in the maker world, if it were possible to ECM metals at a small scale:

- Zero tool wear. The tool doesn't come in contact with the workpiece, it simply advances towards the metal while chemically eroding material away at the same rate.
- No tool marks or burrs
- No large forces on the workpiece or the tool, which makes it possible to machine very delicate structures
- ECM is virtually silent (the only noise is produced by a few pumps)
- No heat affected zone, and no heat-treating equipment required for annealing / rehardening
- Theoretically high accuracy (though, we'll get to that later)

ECM is scarcely seen outside of industry, and truly is a technology that seems to have gotten stuck in the 1950s. Part of the reason for that is, making ECM tools has always been challenging and expensive. The ECM tools themselves have to be conventionally machined out of metal (usually conductive copper), and work kind of like sinker E**D**M, in that they have the inverse shape to the part you want to cut.

<img src="https://i.imgur.com/RgAL5J7.png" height="300" title="source: Okuwobi et al."/>

The big difference is that an ECM tool needs to inject pressurized electrolytic fluid, right at the interface between the tool and the workpiece. The electrolyte is the chemical transfer medium that provokes metal ions to cleave off the metal stock, and also flushes the unwanted particles (which quickly form a thick sludge) away at high speed.

From what I can tell, controlling the fluid behavior of the electrolyte through tool design (where the conduits go, etc.) is the main reason ECM is expensive, because there's an unavoidable amount of trial and error involved.

![plants-crave](https://i.imgur.com/fkzxFaT.gif)

So an ECM tool is not really trivial to make. Or hasn't been. But, it's rather easy to make arbitrary 3D shapes with a 3D printer, and copper happens to be one of the easiest metals to plate over plastic parts (plating baths for copper rank only moderately toxic, compared to, say plating chromium). Combine those two things, I thought, and maybe you can take most of the expense out of the tool making step. Maybe, just maybe, it would be possible to electrochemically machine steel stuff in the enforced quietude of my apartment.

I imagined a process where a positive 3D printed "tool" is plated with a very thin layer of metal. Then, these tools could be used in a way similar to sinker EDM, to machine complex net shapes with resin-print-like tolerances, in tough metals like pre-hardened steels. If you wanted to cut a profile, maybe it would be possible to print a "cookie cutter" geometry, where the inside of the cutting tool is insulative and the edge is conductive.

I embarked on this foolhardy journey with only the foggiest understanding of chemistry and electricity. Armed with an SLA printer, a sacrificial RepRap, some plating chemicals, and a general idea of how to use them, I forged into the unknown.  

## Build Overview

<img src="https://i.imgur.com/n45vC1d.gif" style="margin:20px;height:400px;width:225px;" align="right" title="Ram ECM with Suzanne"/>

Ok, not totally unknown. In the past year or two, intrepid souls on the internet have taken it on themselves to use the principles of ECM to cut gun barrel rifling at home. Whether or not you think the end product is worthwhile, the process seems to work.

If these folks can cut helical groves in (hopefully) barrel-grade steel, with what amounts to a wire wrapped plastic churro and some salt water, it didn't seem unreasonable to expect something in the realm of "results" with a copper-coated 3D print.

The rifling process uses a static tool and controls the groove depth by running constant current for a set amount of time, which gradually widens the grooves as the steel closest to the helical wire erodes away. As a starting point, I used the same electrolyte concentration and amperage they do. I'll put the specifics into a wiki page soon after this post goes up.

In sinker ECM, the tool moves towards the workpiece - I've had it moving at a constant rate, though this may not be ideal. It should be possible to dial in the feed-rate of the tool to where it is in a steady-state condition relative to the rate of erosion, and as a result there would be a constant gap distance between the tool and the part.

<img src="https://i.imgur.com/EghvbqZ.png" style="margin:20px;height:900px;"/>

A little about the mechanics of this machine.

## Designing the ECM Tools

<img src="https://i.imgur.com/FtDlYBG.png" height="700" title="Tool Cutaways"/>

## Electroplating Resin

<img src="https://i.imgur.com/z7eNbk9.jpg" style="margin:20px;height:450px" align="right" title="Spray-coated Suzanne Cutter"/>

I used a Caswell copper plating kit, but I've found that a quality silver conductive spray is the key to electroplating plastic parts with any success. Caswell sells a servicable one. The best quality spray I've found is from Pino Technology (a Swiss company with operations in China). If you attempt to plate a plastic part and it fails, most likely you don't have a great conductive layer, and need a better spray coat.

Depending on the plate thickness, plating can have a relatively minimal impact on the dimensions of the part.

<img src="https://i.imgur.com/WGS2In8.png" style="margin:20px;height:512px;width:900px;" align="right" title="Spray-coated Knife Cutter"/>

The inner surface of the cookie cutter needs to be unplated in order to avoid ECM erosion from the middle of the part.

## Results

Right now the ECM is still controlled by an open loop, and requires a lot of babysitting. This bottlenecks experiments I'd like to run to start to relate surface area, cutting speed, and current density.

<img src="https://i.imgur.com/3vxXUz3.jpg" height="700" title="source: imgur.com"/>

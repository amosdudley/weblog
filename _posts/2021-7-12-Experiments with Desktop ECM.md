---
tags: [self-Amos, reprap, ECM, electrochemistry, electroplating]
title: "Cutting Steel with (Electroplated) Plastic"
---
## Experiments in Sinker ECM
![ecmCAD](https://i.imgur.com/asmgMvv.png)

*Schematic of ECM testbed - first machining results at the end of the page*

**Writing in progress... divert your eyes.**

**Note:** If you're interested in ECM and want to get involved with an open-source project to design a useful desktop-scale machine, send me a message on Discord.

**Note 2:** If you have experience with ECM, you will surely see that I am flying by the seat of my pants, making tons of (likely wrong) assumptions that could be rectified with the right reading material. Feel free to let me know in the comments where I can make improvements!

## Cookie Cutters and Rubber Stamps

Electrochemical machining (ECM) is an unusual way of machining hard metals. If you're familiar with electroplating, it's like that, but in reverse. Instead of adding metal to the surface of an object, you remove it in a controlled manner. ECM is used to cut tiny parts very accurately (micromachining), bore holes with very large aspect ratios, and create complex surfaces in hard metals.

ECM has some very interesting advantages compared to "mechanical" machining, which I think would be underexploited in the maker world, if it were possible to ECM metals at a small scale:

- Zero tool wear. The tool doesn't come in contact with the workpiece, it simply advances towards the metal while chemically eroding material away at the same rate.
- No tool marks or burrs
- No large forces on the workpiece or the tool, which makes it possible to machine very delicate structures
- ECM is virtually silent (the only noise is produced by a few pumps)
- No heat affected zone, and no heat-treating equipment required for annealing / rehardening
- Theoretically high accuracy (though, we'll get to that later)

ECM is scarcely seen outside of industry, and truly is a technology that seems to have gotten stuck in time. Part of the reason for that is, making ECM tools has always been challenging and expensive, and that hasn't changed much since the 1950s. The ECM tools themselves have to be conventionally machined out of metal (usually conductive copper), and work kind of like sinker E**D**M, in that they have the inverse shape to the part you want to cut.

<img src="https://i.imgur.com/RgAL5J7.png" height="300" title="source: Okuwobi et al."/>

The big difference is that an ECM tool needs to inject pressurized electrolytic fluid, right at the interface between the tool and the workpiece. The electrolyte is the chemical transfer medium that provokes metal ions to cleave off the metal stock, and also flushes the unwanted particles (which quickly form a thick sludge) away at high speed.

From what I can tell, controlling the fluid behavior of the electrolyte through tool design (where the conduits go, etc.) is the main reason ECM is expensive, because there's an unavoidable amount of trial and error involved.

![plants-crave](https://i.imgur.com/fkzxFaT.gif)

So an ECM tool is not really trivial to make. Or hasn't been. But, it's rather easy to make arbitrary 3D shapes with a 3D printer, and copper happens to be one of the easiest metals to plate over plastic parts (plating baths for copper rank only moderately toxic, compared to, say plating chromium). Combine those two things, I thought, and maybe you can take most of the expense out of the tool making step. Maybe, just maybe, it would be possible to electrochemically machine steel stuff in the enforced quietude of my apartment.

I imagined a process where a positive 3D printed "tool" is plated with a very thin layer of metal. Then, these tools could be used in a way similar to sinker EDM, to machine complex 3D shapes in tough metals like pre-hardened steels. I'm also curious if it's possible to print a "cookie cutter" geometry, where only the edge of the tool is conductive, in order to cut profiles similar to a waterjet with a much smaller footprint.

I embarked on this foolhardy journey with only the foggiest understanding of chemistry and electricity. Armed with an SLA printer, a sacrificial RepRap, some plating chemicals, and a general idea of how to use them, I forged into the unknown.  

## Build Overview

<img src="https://i.imgur.com/n45vC1d.gif" style="margin:20px;height:400px;width:225px;" align="right" title="Ram ECM with Suzanne"/>

Ok, not totally unknown. In the past year or two, intrepid souls on the internet have taken it on themselves to use the principles of ECM to cut gun barrel rifling at home. Whether or not you think the end product is worthwhile, the process seems to work.

If these folks can cut helical groves in (hopefully) barrel-grade steel, with what amounts to a wire wrapped plastic churro and some salt water, it didn't seem unreasonable to expect something in the realm of "results" with a copper-coated 3D print. The rifling process uses a static tool and controls the groove depth by running constant current for a set amount of time, which gradually widens the grooves as the steel closest to the helical wire erodes away. As a starting point, I used the same electrolyte concentration, pumping equipment, and amperage they do. I'll put the specifics into a wiki page soon after this post goes up.

I've put a diagram of the machine at the top of the article. It's quite a simple Z motion platform, geared down to make it possible to move very small increments. The toolhead is rigidly attached to the motion stage, with a "crown gear" pivot point to allow the tool to be rotated up and back into place manually for installation. I 3D printed a platform for holding the metal stock over a plastic capture tank. There's also a second plastic bin thats used as a cover, because pumping pressurized salt water between the tool and the stock causes a lot of overspray. I used a large glass beaker as a secondary holding tank to experiment with electrolyte filtration, and as a way to more easily replace the solution mid-cut if necessary without jostling the machine.

Electrolyte is pumped through the tool with a $40 micro-diaphragm pump, and returns to the capture tank with a cheap aquarium pump. Both these pumps seem to be fairly robust against getting clogged by ECM sludge, which at first seemed likely to become a problem. The amount of flow from the two pumps is not balanced (the injection flow gets constricted at the toolhead), but the aquarium pump has no trouble pumping without full submersion - so it just maintains the waterline in the capture tank.  

<img src="https://i.imgur.com/EghvbqZ.png" style="margin:20px;height:900px;"/>
*Most of the non-8020 parts are "Tough 2000" resin, but everything should be printable with FDM as well.*

The motion stage is driven by a CNC Shield on an Arduino Mega running GRBL, because that's what I had laying around. The 5:1 geared steppers + Tr8x2 leadscrews (2mm pitch) provide a truly unnecessary Z resolution of ~8145 steps/mm. Feed rates in real ECM vary from 0.5 to 15 mm min, but given my small power source I started at 1/10th that speed (50 microns/min). Unfortunately it seems like there's a relatively high hard coded minimum feed rate in GRBL 0.8, so I wasn't able to just run single G-Code moves at the very slow rate I wanted. My workaround (in lieu of getting a better controller) was to write a little script to generate G-Code defining the overall move as a series of tiny steps (1 microstep) and waits. It also inserts lift/return moves at periodic intervals, in hopes that this would help with flushing ECM sludge (more on that later).

The two pumps are powered by a cheap PC power supply, with a manual kill switch. Power for the ECM cutting is delivered by a 30V 10A <a href="https://www.amazon.com/gp/product/B087TK6ZM2/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B087TK6ZM2&linkCode=as2&tag=amosdudley-20&linkId=ea429096fd7fd0e34136f10c625cdce2">30V 10A bench power supply</a> in constant current mode, with the current set to 7.5A.

An obvious next step for this project is to synchronize pump activation + ECM current + tool motion. The last two are especially important - I found that voltage seems to vary as a function of gap distance and active surface area (the region between the tool and the workpiece that would be touching if you closed the gap), which implies that some of the issues I had with tools crashing into the workpiece could be remedied by dynamically slowing feed rate as voltage drops (with a multiplier from a table of surface areas over cut depth that is pre-calculated from the model)

## Filtration


## Designing the ECM Tools

<img src="https://i.imgur.com/FtDlYBG.png" height="700" title="Tool Cutaways"/>

## Electroplating Resin

<img src="https://i.imgur.com/z7eNbk9.jpg" style="margin:20px;height:450px" align="right" title="Spray-coated Suzanne Cutter"/>

I used a Caswell copper plating kit, but I've found that a quality silver conductive spray is the key to electroplating plastic parts with any success. Caswell sells a servicable one. The best quality spray I've found is from Pino Technology (a Swiss company with operations in China). If you attempt to plate a plastic part and it fails, most likely you don't have a great conductive layer, and need a better spray coat.

Depending on the plate thickness, plating can have a relatively minimal impact on the dimensions of the part. I needed between 25-50 microns of copper to survive ECMing through at least 5mm of material (mainly, it just needs to survive occasionally crashing into the workpiece).   

<img src="https://i.imgur.com/WGS2In8.png" style="margin:20px;height:512px;width:900px;" align="right" title="Spray-coated Knife Cutter"/>

The inner surface of the cookie cutter needs to be unplated in order to avoid ECM erosion from the middle of the part.

## Results
In "Sinker ECM
," the tool moves towards the workpiece - I've had it moving at a constant rate, though this may not be ideal. It should be possible to dial in the feed-rate of the tool to where it is in a steady-state condition relative to the rate of erosion, and as a result there would be a constant gap distance between the tool and the part.

Right now the ECM is still controlled by an open loop, and requires a lot of babysitting. This bottlenecks experiments I'd like to run to start to relate surface area, cutting speed, and current density.

<img src="https://i.imgur.com/3vxXUz3.jpg" height="700" title="source: imgur.com"/>

---
tags: [self-Amos, reprap, ECM, electrochemistry, electroplating]
title: "Cutting Steel with (Electroplated) Plastic"
---
## Experiments in Sinker ECM
![ecmCAD](https://i.imgur.com/asmgMvv.png)

*Schematic of ECM testbed - first machining results at the end of the page*

**Writing in progress... divert your eyes.**

**Note:** If you're interested in ECM and want to get involved with an open-source project to design a useful desktop-scale machine, send me a message on Discord.

**Note 2:** If you have experience with ECM, you will surely see that I am flying by the seat of my pants, making tons of (likely wrong) assumptions that could be rectified with the right reading material. Feel free to let me know in the comments how I can make improvements!

## Stamps and Cookie Cutters

Electrochemical machining (ECM) is an unusual way of machining hard metals. If you're familiar with electroplating, it's like that, but in reverse. Instead of adding metal to the surface of an object, you remove it in a controlled manner. ECM is used to cut tiny parts very accurately (micromachining), bore holes with very large aspect ratios, and create complex surfaces in hard metals.

ECM has some very interesting advantages compared to "mechanical" machining, which I think would be underexploited in the maker world, if it were possible to ECM metals at a small scale:

- Zero tool wear. The tool doesn't come in contact with the workpiece, it simply advances towards the metal while chemically eroding material away at the same rate.
- No tool marks or burrs
- No large forces on the workpiece or the tool, which makes it possible to machine very delicate structures
- ECM is virtually silent (the only noise is produced by a few pumps)
- No heat affected zone, and no heat-treating equipment required for annealing / rehardening
- Theoretically high accuracy (though, we'll get to that later)

ECM is scarcely seen outside of industry, and truly is a technology that seems to have gotten stuck in time. Part of the reason for that is, making ECM tools has always been challenging and expensive, and that hasn't changed much since the 1950s. The ECM tools themselves have to be conventionally machined out of metal (usually conductive copper), and work kind of like sinker E**D**M, in that they have the inverse shape to the part you want to cut.

<img src="https://i.imgur.com/RgAL5J7.png" title="source: Okuwobi et al." style="margin:20px;height:80%;width:80%;">

The big difference is that an ECM tool needs to inject pressurized electrolytic fluid directly at the interface between the tool and the workpiece. The electrolyte is the chemical transfer medium that provokes metal ions to cleave off the metal stock, and also flushes the unwanted particles (which quickly form a thick sludge) away at high speed.

From what I can tell, controlling the fluid behavior of the electrolyte through tool design (where the conduits go, etc.) is the main reason ECM is expensive, because there's an unavoidable amount of trial and error involved.

![plants-crave](https://i.imgur.com/fkzxFaT.gif)

So an ECM tool is not really trivial to make. Or hasn't been. But, it's rather easy to make arbitrary 3D shapes with a 3D printer, and copper happens to be one of the easiest metals to plate over plastic parts (plating baths for copper rank only moderately toxic, compared to, say plating chromium). Combine those two things, I thought, and maybe you can take most of the expense out of the tool making step. Maybe, just maybe, it would be possible to electrochemically machine steel stuff in the enforced quietude of my apartment.

I imagined a process where a positive 3D printed "tool" is plated with a very thin layer of metal. Then, these tools could be used in a way similar to sinker EDM, to machine complex 3D shapes in tough metals like pre-hardened steels. I was also curious if it's possible to print a "cookie cutter" geometry, where only the edge of the tool is conductive, in order to cut profiles similar to a waterjet with a much smaller footprint.

I embarked on this foolhardy journey with only the foggiest understanding of chemistry and electricity. Armed with an SLA printer, a sacrificial RepRap, some plating chemicals, and a general idea of how to use them, I forged into the unknown.  

## Build Overview



Ok, not totally unknown. In the past year or two, intrepid souls on the internet have taken it on themselves to use the principles of ECM to cut gun barrel rifling at home. Whether or not you think the end product is worthwhile, the process seems to work.

If these folks can cut helical groves in (hopefully) barrel-grade steel, with what amounts to a wire wrapped plastic churro and some salt water, it didn't seem unreasonable to expect something in the realm of "results" with a copper-coated 3D print. The rifling process uses a static tool and controls the groove depth by running constant current for a set amount of time, which gradually widens the grooves as the steel closest to the helical wire erodes away. As a starting point, I used the same electrolyte concentration, pumping equipment, and amperage they do. I'll put the specifics into a wiki page soon after this post goes up.

I've put a diagram of the machine at the top of the article. Mainly, it's a simple Z motion platform, geared down to make it possible to move very small increments. The toolhead is rigidly attached to the motion stage, with a "crown gear" pivot point to allow the tool to be rotated up and back into place manually for installation. I 3D printed a platform for holding the metal stock over a plastic capture tank, which seems to be rigid enough for the current purpose.

A second plastic bin covers the top, because electrolyte injection causes a lot of overspray (which is corrosive to the leadscrews & rails). I repurposed a large glass beaker as a secondary holding tank to experiment with electrolyte filtration, and as a way to more easily replace the solution mid-cut if necessary without jostling the machine.

Electrolyte is pumped through the tool with a $40 micro-diaphragm pump, and returns to the capture tank with a cheap aquarium pump. Both these pumps seem to be fairly robust against getting clogged by ECM sludge (and are fairly easily cleaned). The amount of flow from the two pumps is not balanced - the input flow gets constricted at the toolhead. Luckily, the aquarium pump has no trouble pumping without full submersion, and it happily maintains a constant waterline in the capture tank.  

<img src="https://i.imgur.com/EghvbqZ.png" style="margin:20px;height:100%;width:100%;">
*Most of the non-8020 parts are "Tough 2000" resin, but everything should be printable with FDM as well.*

<img src="https://i.imgur.com/n45vC1d.gif" style="margin:20px;height:355px;width:200px;" align="right" title="Ram ECM with Suzanne"/>

The motion stage is driven by a CNC Shield on an Arduino Mega running GRBL, because that's what I had laying around. The 5:1 geared steppers + Tr8x2 leadscrews (2mm pitch) provide a truly unnecessary Z resolution of ~8145 steps/mm. Feed rates in real ECM vary from 0.5 to 15 mm min, but given my small power source I started at 1/10th that speed (50 microns/min). Unfortunately it seems like there's a relatively high hard coded minimum feed rate in GRBL 0.8, so I wasn't able to just run single G-Code moves at the very slow rate I wanted. My workaround (in lieu of getting a better controller) was to write a little script to generate G-Code defining the overall move as a series of tiny steps (1 microstep) and waits. It also inserts lift/return moves at periodic intervals, in hopes that this would help with flushing ECM sludge (more on that later).

The two pumps are powered by a cheap PC power supply, with a manual kill switch. Power for the ECM cutting is delivered by a 30V 10A <a href="https://www.amazon.com/gp/product/B087TK6ZM2/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B087TK6ZM2&linkCode=as2&tag=amosdudley-20&linkId=ea429096fd7fd0e34136f10c625cdce2">30V 10A bench power supply</a> in constant current mode, with the current set to 7.5A.

I know for certain that ECM generates hydrogen gas, which can be seen as bubbles forming at the cutting interface. A small amount of chlorine is also likely being generated (based on the smell). So, just in case, I'm running the ECM in a ventilated box (a paint hood), with the electronics board & power supply outside the box.

## Filtration

<img src="https://i.imgur.com/nX4YqbU.gif" style="margin:20px;height:40%;width:40%;" align="right" title="Sludge Settling"/>

I wasn't prepared for how quickly ECM produces waste sludge. This sludge is the product of the reaction of the separated components of the work steel and the electrolyte. I'd like to mention at this point that ECM byproducts can be toxic, depending on the composition of the alloy. If the steel contains chromium (ie stainless and others), one of these byproducts might be hexavalent chromium, which is carcinogenic. So please, don't try this at home with chromium-containing alloys. My experiments thusfar have been with A36 and 1095 carbon steel. These steels are iron alloyed with manganese, carbon, silicon, copper, sulphur and phosphorous. Which doesn't mean there aren't other hazardous byproducts being formed, but I'm blissfully unaware (and wear gloves).

The ECM sludge is reddish brown and agglomerates slightly over time. Maybe sludge is a bad description - it's denser than the saltwater solution, but the particle size is so small that it takes a while to settle out. A few internet sources suggest that most of this sludge is iron (II) hydroxide or possibly Iron (III) oxide-hydroxide, or maybe even rust, which are safe and insoluble.

The main problem caused by ECM sludge seems to be when it builds up on the workpiece. After my ECM runs undisturbed for ~10min, I find that the cutting interface is often partially coated in a black residue. It's easily cleaned off with a wire brush or wiped off with a finger.

This residue insulates, or at least physically masks, the steel below it, and causes regions below it to remain as un-eroded high points in the machining operation. When ECM isn't uniformly eroding material, you get a crash - where the tool collides with those high points, creating a short circuit.  

I'm not certain whether the black residue has the same composition as the reddish suspended particles, but it's a problem. If it is the same, it might be caused by reaching some critical concentration of sludge in the electrolytic solution, since I'm recirculating this fluid many times. I tried a few different methods of filtering the sludge to combat this, but none have worked:

- Layered cotton fabric in an in-line filter
- Activated carbon filtration 
- Centrifugal separation with a 3D printed hydrocyclone manifold

<img src="https://i.imgur.com/77a8eWW.png" title="Hydrocyclone Manifold" style="margin:20px;width:100%;">

I was very surprised that activated carbon had virtually no filtration power with ECM sludge. The hydroxide particles must be incredibly small. I tested this independently of the ECM, and there was no visible change in the level of settled sludge after four hours of filtering. Although kind of neat, the hydrocyclone was clearly just mixing the sludge into suspension rather than doing any separation. The difference in densities is just too small for it to work, at least at this scale.

A better way to separate and filter the sludge might be with gravity: two holding tanks, with servo-operated valves to divert the loop to the "active" tank, while the other settles and the waste is sep-funneled away.

## Designing ECM Tools

<img src="https://i.imgur.com/FtDlYBG.png" title="Tool Cutaways" style="margin:20px;width:80%;">

## Electroplating Resin

<img src="https://i.imgur.com/z7eNbk9.jpg" style="margin:20px;width:50%;" align="right" title="Spray-coated Suzanne Cutter">

I'm not going to go too deep into how to plate stuff here. <a href="https://caswellplating.com/">Caswell</a> sells a guide that's detailed and helpful, if a little dated. I used a Caswell copper plating kit, but I've found that a quality silver conductive spray is the key to electroplating plastic parts with any success.

The best quality spray I've found is from Pino Technology (a Swiss company that sells from China). If you attempt to plate a plastic part and it fails, most likely you don't have a great conductive layer, and need a better spray coat.

Depending on the plate thickness, plating can have a relatively minimal impact on the dimensions of the part. I found I needed between 25-50 microns of copper to survive  occasionally crashing into the workpiece.   

<img src="https://i.imgur.com/WGS2In8.png" style="margin:20px;width:95%;" title="Spray-coated Knife Cutter">

In theory, the inner surface of the cookie cutter needs to be unplated in order to avoid ECM erosion removing material from middle of the "cookie" (everything inside the profile). I tried to accomplish this by printing a plug that would mask off the inside of the cutter.

This didn't work as well as I'd hoped, and I ended up just spray-coating the whole thing, and then scribing the inside edge of the cutter to break electrical connectivity with the inner (now conductive) surface.

## Results
In "Sinker ECM," the tool moves towards the workpiece -

I've had it moving at a constant rate, though this may not be ideal. It should be possible to dial in the feed-rate of the tool to where it is in a steady-state condition relative to the rate of erosion, and as a result there would be a constant gap distance between the tool and the part.

Right now the ECM is still controlled by an open loop, and requires a lot of babysitting. This bottlenecks experiments I'd like to run to start to relate surface area, cutting speed, and current density.

<img src="https://i.imgur.com/3vxXUz3.jpg" title="Impression of Suzanne in A36 Steel" style="margin:20px;width:80%;">

## Further work

An obvious next step for this project is to synchronize pump activation + ECM current + tool motion. The last two are especially important - I found that voltage seems to vary as a function of gap distance and active surface area (the region between the tool and the workpiece that would be touching if you closed the gap), which implies that some of the issues I had with tools crashing into the workpiece could be remedied by dynamically slowing feed rate as voltage drops (with a multiplier from a table of surface areas over cut depth that is pre-calculated from the model).

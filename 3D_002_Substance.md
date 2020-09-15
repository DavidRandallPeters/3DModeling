# 3D Modeling for Game | 002 | Substance Painter


![Atom Can](https://user-images.githubusercontent.com/36719180/93180373-29155480-f78b-11ea-9d91-59c89a6adb45.png)


Notes prepared by David Peters

Using Maya 2020

---

## 002.001 | Overview of this tutorial

<br>

The process we'll undergo follows.

Note that this is an express rendition that will get us quickly into the fun stuff and out the other side.

There are additional tips and tricks that we'll get into another day.

<br>

1. Begin in Maya - prepare both high- and low-poly meshes for export and baking
2. Export models as .fbx
3. Export UV map for Photoshop
4. Fire up Substance and import low-poly model
5. Bake all maps using the high-poly model as a source
6. Apply materials
7. Add an emissive channel for glowing stuff
8. Use alpha brushes
9. Add custom alphas

<br><br>

---

## 002.002 | Normal maps

<br>

![Ceres normal map](https://user-images.githubusercontent.com/36719180/93048659-8211b980-f6b3-11ea-8281-03e376bb5a10.png)

When preparing 3D assets for use in game engines, we need to save on resources wherever possible. This means working to lighten the processing load by keeping assets light-weight.

You'll have heard the terms *low-poly* and *high-poly* before, no doubt.

In case you're unfamiliar with these terms, we're talking about the polygon count of a 3D mesh. A model's polys can number into the tens of thousands, depending on how it was created and to what detail. Typically, soft-surface models (eg. organic creatures) created in sculpting software (such as ZBrush) will reach these lofty heights - hard-surface models absolutely can too.

It would be a shame if the detail that we achieve when modeling or sculpting was wasted in the process of preparing our assets for use in a game. Fortunately, it doesn't have to be..

Substance Painter has the capability of *'baking'* the detail of a high-poly mesh down to a low-poly mesh. This means that grooves and rivets and creases and wrinkles can be included in what's called a *normal map* - (derived from the high-poly model) - which is projected onto a light-weight low-poly model.

A normal map 'weighs' only as much as a 2D texture, but when read by 3D software and indeed game engines, can massively improve the fidelity of a low-poly model.

<br>

![Normal example](https://user-images.githubusercontent.com/36719180/93049109-71157800-f6b4-11ea-8ab4-2756cc63a41c.png)

<br>

The mesh on the right in this picture is the same as the mesh on the left - (that is, they both have the same number of polys) - but a highly detailed mesh has been projected onto the mesh on the right as a normal map. By precaulclating where light should hit and shadows be cast, it gives the appearance of a mesh with much more detail.

<br><br>

---

## 002.002 | High-poly and Low-poly models in Maya

<br>

This break-down assumes that you even desire high-mesh detail to be baked onto a low-poly mesh. This tutorial will still inform you of the Maya » Substance workflow even if you only have the one [low-poly] mesh.

That said, I do suggest you follow these instructions in the interests of absorbing the skills.

<br>

Typically, you'll begin with a high-poly model, duplicate it and decimate it (or otherwise simplify the mesh) resulting in a low-poly version that shares the same dimensions and world-space. However, there's no reason you can't work in the other direction - adding detail to a low-poly mesh.

<br>

The main things to note are that:

1. There are indeed two versions of the asset
2. They do occupy the same world-space
3. They share the same overall dimensions

<br>

I'll continue using the landmine model from last time.

For the purposes of this tutorial, I suggest you do the same - *regardless of whether or not you have your own model to work with.*

Once you have the basics down, you can go back and try it out with your own model.

<br>

I've provided a new Maya scene that contains both high-poly and low-poly iterations of the landmine.

<br>

- Download the new scene now and open it in Maya
- Ensure that the **Channel Box/Layer Editor** tab is active

<br>

You're presented with the *high-poly* version of the landmine model.

<br>

![High-poly landmine](https://user-images.githubusercontent.com/36719180/93149242-f0a15680-f749-11ea-970a-69d353621a57.png)

<br>

- Select the model and explore its detail - there's a dent in the shell, joins and depressions
- Open the **UV Edito**r and notice that it's a mess in there! This is fine. We're only interested in the low-poly model's UV map
- In the **Layers** section (at the bottom of the **Channel Box/Layer Editor**), hit the **V** to the right of **HighPoly** layer to make that layer and its contents invisible

<br>

![Layers](https://user-images.githubusercontent.com/36719180/93149451-7c1ae780-f74a-11ea-9501-f323680b56e5.png)

<br>

- Do the inverse for the **LowPoly** layer - making it visible
- Notice that the low-poly and high-poly meshes share the exact same world-space - *this is very important for accurate projection!*
- Take a moment to explore the *UV Shells* of the model in the **UV Editor** and close it when you're ready

<br>

![Low-poly shells](https://user-images.githubusercontent.com/36719180/93149698-33176300-f74b-11ea-92c4-d670f6990027.png)

<br>

- Hop into **Object mode** and select the **low-poly** object
- Notice that it still has all of its history
- Delete its History (**Edit » Delete by Type » History** or use the corresponding button in the **Poly Modeling toolset**)

<br><br>


---

## 002.003 | Committing smooth preview

<br>

You'll be aware already of the *1*, *2* and *3* hotkeys - when an object is selected, those keys allow us to cycle between an accurate [unsmoothed] presentation of that object and an *innacurate* preview of what that mesh *would* look like if were to apply / commit smoothness.

But who ever does that?

**We do** - because we want ALL of the detail and we want it at its finest.

<br>

- With the high-poly mesh selected hit **1** to show the object as it truly is
- Choose **Mesh » Smooth** (from the top menu bar) - choose the default **1** division
- Hit **Q** to apply

<br>

If we were to hit *3* now, Maya would likely give us a warning:

>"The selected mesh [blah] contains a large number of faces and may take a while to smooth or run our of memory. Do you want to continue with smooth mesh preview?"

No. We do not. That would mean *smoothing the smoothness* - resulting in a silly number of polys - and we already have quite enough.

<br>

- Now that that's done, also delete the high-poly object's history

<br><br>

---

## 002.004 | Establishing common / grounded pivots

<br>

This next bit isn't for the benfit of Substance but for your chosen game engine (in this case, Unreal).

This is a good habit to get into for two reasons:

<br>

> 1. For the purpose of assembling complex models (with multiple components) quickly, in-engine. <br> <br> Imagine you have a table asset that has a bunch of beer mugs and swords on it (let's assume that these can't be picked up - this approach will oftentimes be irrelevant for collectible items as they would typically require a centered pivot). <br> <br> These mugs and swords are bound to be separate components (and ultimately separate 3D assets) - not least because the contents of the table may vary from scene to scene (or from table to table). <br> <br> To assist with rapid assembly in-engine, we can establish common pivot points for all items, here in Maya - meaning that we can literally drag and drop each varied (and variable) asset and they'll assemble perfectly without fiddly manipulation. Table/item combinations can then be saved as varied Prefabs (Unity) or Blueprints (Unreal).

<br>

> 2. So that when objects are placed or instantiated in-engine, they'll instantiate *above* the ground-plane - not in the middle of it.

<br><br>

So. Let's get this skill down:

<br>

- Hit **Space** and choose one of the side orthographic projections
- Select the object, hit **W** (move) and notice that its pivot is currently centered
- Hit **D** - the gizmo changes its appearance - we are now able to move that pivot

<br>

![Pivot centered](https://user-images.githubusercontent.com/36719180/93152419-d6b84180-f752-11ea-9bda-509e6d57f1cc.png)

<br>

- Hold **X** to snap to points, click and drag the *yellow* part of the gizmo until the pivot rests at **'origin'** (0,0,0)

<br>

![Pivot moved](https://user-images.githubusercontent.com/36719180/93152422-d91a9b80-f752-11ea-9bea-af62adab870a.png)

<br>

- Again, hit **D** to switch back to normal *move* mode
- *Repeat* these steps for the **high-poly** mesh

<br>

It should go withoutsaying that When doing this for your own model, ensure you do this for each and every component / object in your asset.

<br><br>

---

## 002.005 | Exporting models from Maya

<br>

This part's quite easy - all preparations have now been made and it's only a matter of getting these models into a folder for import to Substance.

Note that the UV maps will be exported with the model as part of this process - and we'll just use the low-poly UV map.

<br>

- Select the **low-poly** object in the viewport
- Choose **File » Export Selection**
- Ensure the model is going to a sensible folder location
- Give the model a descriptive file name - eg.: *LandMineHigh001*
- Ensure that the **Files of type:** field is set to **FBX export**
- Default *Options* will be fine
- Hit **Exprt Selection**

<br>

- Repeat these steps for your **high-poly** object - (of course, adjusting the file name appropriately)

<br><br>

---

## 002.006 | To Substance

<br>

I think we can all agree that this is the fun part.

Let her rip!

<br>

- We're done with Maya, so you can close that if you wish
- Open **Substance Painter**
- We're likely presented with a *Welcome* panel. You can close that.
- In the top menu bar, choose **File » New** - we see the *New Project* panel
- Set the **Template** to **Unreal Engine 4 (allegorithmic)** - (but note that there is also a *Unity* template)
- Just beneath the *Template* section it says *File* - hit the **Select** button to the right of this
- Locate your exported **low-poly** .fbx mesh and hit **Open**
- Set the **Document Resolution** to **2k** (**2048**) - this determines the resolution of your textures and maps
>Note that this is not a final commitment - the Substance Painter workflow is non-destructive - meaning that texture resolutions can be increased or decreased later
- Hit **OK**

<br>

The top-half of your screen should look something like this:

<br>

![Open Substance](https://user-images.githubusercontent.com/36719180/93154066-cd30d880-f756-11ea-95dc-c504b2c4fa01.png)

<br>

Below that are butt-loads of brushes, alphas, presets and various parameters.

<br>

---

## 002.007| Environment settings

<br>

First up, we'll look at Environment settings. 

Currently, the background in our viewport is blank.

But we can light up an HDRI background that roughly resembles the environment in which our asset will ultimately be placed.


- In the far *top-right* of the screen, locate the **Display Settings** button - (it's the top-most of three buttons)
- Open **Display Settings** - at the top of the panel is *ENVIRONMENT SETTINGS*
- Dial up the **Environment Opacity** slider - a blurry background will appear in the viewport
- Reduce the **Environment Blur** to see what you're lookin' at - *sunny pastures!*

<br>

![Sunny pastures](https://user-images.githubusercontent.com/36719180/93155083-5d701d00-f759-11ea-95ce-921d43486d5f.png)

<br>

The lighting that's applied to the model is derived from this HDRI background using a kind of *Global Illumination (GI)* - we'll change this background to ensure that our paint-job works in our target environment - which let's pretend is a darker industrial environment..

<br>

- Hit the button next to **Enironment Map** and select another image. I'm going with **Gdansk Shipyard Buildings** - the image changes
- Adjust the **Blur** and **Exposure (EV)** as you see fit
- **Explore** the other settings in this panel and **close it** when you're ready

<br><br>

---

## 002.008 | Baking high-poly to low-poly

<br>

This is the magic bit. We're about to take the high-poly detail and project it onto our low-poly mesh.

<br>

- In the **TEXTURE SET SETTINGS** panel (right-hand side of screen), scroll down until you find the **MESH MAPS** category
- Hit the **Bake Mesh Maps** button - the *Baking* panel pops up
- Adjust the **Output Size** to match your document (**2048**)
- Hit the little file-lookin' button indicated in the image below (**High definition meshes** is its tooltip)
- Locate and select your **high-poly** mesh and hit **Open**

<br>

![Baking](https://user-images.githubusercontent.com/36719180/93156678-b9887080-f75c-11ea-93db-5ff820ebd984.png)

<br>

- The **Max Frontal Distance** and **Max Rear Distance** settings will vary depending on your model - you may wish to come back in here later, change those settings and rebake - depending on results (mesh details may not always bake nicely). For now, dial them both up to **1** and see how you go.
- Hit **Bake selected textures**

<br>

Substance will run a bunch of calculations - hopefully resulting in a yummy projection:

<br>

![Baked](https://user-images.githubusercontent.com/36719180/93156786-f2284a00-f75c-11ea-8bce-e315c6942c53.png)

<br>

To see for ourselves that this is more than just lines on a surface, we'll rotate the sun's position in the sky and watch as the shadows are cast appropriately - despite there being *no additional mesh detail..*

<br>

- With your mouse cursor in the main viewport, hold **Shift** + **Right mouse button** and drag from side-to-side
> Pay close attention to the depressions in the top of the shell..
<br>

*RIGHT???*

<br><br>

---

## 002.009 | Applying materials in Substance

<br>

Okay, okay - let's paint already.

<br>

### Base layer

<br>

This first bit's real easy.

<br>

- Browse the **Materials** bin in the **SHELF** at the bottom of the screen for a suitable 'metal' base - I'm going with **Iron Raw Damaged**
- Drag your chosen base material directly onto the model in the viewport

<br>

![Metal base](https://user-images.githubusercontent.com/36719180/93157476-69121280-f75e-11ea-8c49-4f869c3562b9.png)

<br>

- In the top-right of your screen, tab over to **LAYERS** - (currently, we're in *TEXTURE SET SETTINGS*)

<br>

Notice, in the LAYERS panel that *Iron Raw Damaged* is a *Fill* layer - positioned on TOP of the 'stack'.

The layers, here, work the same way as in Photoshop; what's on top is.. on top.

There's a now-redundant layer on the bottom of the stack called *Layer 1*. 

<br>

- Select **Layer 1** and hit the **trash-can** button to remove that layer - keeping things clean

<br><br>

### Smart Materials

<br>

Subsequent layers inherit some properties from those below. *Normal maps* are case in point - if there is any height information in our base coat (don't worry, there isn't) that will combine show all the way to the top. The same is true of any additional layers that we add.

*This is a good thing!* It allows us to concoct materials that look like paint that's painted over rust - which is painted over paint that's painted over rust.

That cumulative effect is part of why Substance Painter is so cool. But it's also something to keep track of as you build your textures.

<br>

Let's add some actual paint:

<br>

- In the **SHELF**, bottom-left of the screen, locate and select **Smart Materials** - these are materials with added parameters for more control

- Browse the bin (once it loads) and choose a suitable paint *smart material* - I'm going with **Steel Painted Scraped Green**

> Notice that this material looks for hard edges and exposes metal beneath the paint in those areas to simulate wear and tear

<br>

![Steel painted 01](https://user-images.githubusercontent.com/36719180/93161963-d0809000-f767-11ea-8a3d-0ca1662021c3.png)

<br><br>

I had my heart set on a yellowy orange for this paint - so let's change the colour..

<br>

- Hit the **Folder** icon to the left of the **Steel Painted Scraped Green** layer in the **Layers** panel

> Have a quick look at the various other layers that this *smart layer* is comprised of

- Locate **Base Metal** and select it

- In the bottom-right of the screen, locate the **PROPERTIES - FILL** panel

- Scroll down until you find the **Base Color** swatch and hit it

- Adjust the *base color* as you see fit

<br>

![Too much grime](https://user-images.githubusercontent.com/36719180/93162448-e93d7580-f768-11ea-87e1-7c30b81d4268.png)

<br>

It's now more apparent that Substance has gone way OTT on the 'grime'. A little subtly, please, folks!

Let's dial that back some.

<br>

- Zoom in a little on your landmine so that we can see the following changes clearly

- Hit the **eye** icon (to the left of each constituent layer) off and on again to get a feel for what they each do

- It's the **Dirt** layer that's upsetting me .. in that layer, there are two swatches. Select the **swatch** on the **right**

- From the options that become available, select **Grunge Scratches Rough** - its properties become available in the *PROPERTIES - FILL* panel

<br>

![Grunge](https://user-images.githubusercontent.com/36719180/93162996-1f2f2980-f76a-11ea-90cb-fc0ba3186c66.png)

<br>

- In the **PROPERTIES - FILL** panel, fiddle around with parameters until you like what you see - the main parameter I'm interested in is **Balance** - I'm dialling that back

<br>

Things are looking somewhat less garish.

<br>

![Better paint](https://user-images.githubusercontent.com/36719180/93163415-37ec0f00-f76b-11ea-8255-c1391bf09487.png)

<br><br>

### Masking

<br>

In order to expose that lovely damaged iron that we used as a base, we need to employ masks.

Masks allow us to block regions of a fill and allow others through.

We'll block this yellow paint where we want to see metal.

<br>

- In the **LAYERS** panel, hit the folder icon next to **Steel Painted Scraped Green** to minimise its contents

- Double-click the words **Steel Painted Scraped Green** and rename it to something like *Yellow Paint*

- Still in the **LAYERS** panel, hit the **Add mask** button (second from the left)

- Choose **Add black mask** - the paint disappears

> As you see, BLACK blocks the layer - while WHITE allows it through.

- The cleanest way to do this next bit is by using the **Polygon Fill** tool - select it from the main tool bar on the far left of the screen

> You should now see your mesh detail projected on the model in the viewport

- In the **PROPERTIES - POLYGON FILL** panel, ensure that the fill **Color** is set to full **white** (drag the slider all the way to the right)

> You can absolutely start working directly on your model - but the faster, less fiddly method is by working with your UV map

- In the **UV Map**, click in any mesh cell that you want to become 'painted' - the paint is let through

> You can totally click to your heart's content - but we can nail this in one fell swoop

- In the **UV Map**, drag a selection marquee across the long rectangular strips that represent the band around the landmine

<br>

![Yellow band](https://user-images.githubusercontent.com/36719180/93164578-f741c500-f76d-11ea-8e0c-0edb2ec02741.png)

<br>

- Continue in this way until everything that you'd like 'painted' is indeed 'painted'

<br>

![Painted](https://user-images.githubusercontent.com/36719180/93164930-d3cb4a00-f76e-11ea-8d3b-d1253b40b94f.png)

<br><br>

### Emissive materials

<br>

We all love glowy stuff. Amiright?

Let's add glowy stuff.

To get this up and running, we need to first add a channel that's dedicated to emission.

<br>

- Tab over to **TEXTURE SET SETTINGS** (next to the *LAYERS** panel)

- Locate the **CHANNELS** section

- Hit the lil' **+** button on the right-hand side of this section

- Choose **Emissive** from the list that appears

- Tab back over to the **LAYERS** panel

- Hit the **Add a fill layer** button (fourth from the left at the top of this panel) - this adds a white fill layer to the top of the stack

- Rename the layer to something like *Emissive Red*

- In the **PROPERTIES - FILL** panel, locate the **MATERIAL** section

> Notice that all channels are enabled - indicated by a blue border

- Switch off all channels except **emiss**

- Scroll down within that same panel and locate the **Emissive** swatch and hit it

- Choose a colour for your glowy stuff

<br>

![Glowy 01](https://user-images.githubusercontent.com/36719180/93165820-31f92c80-f771-11ea-8038-45b6b1e7fce9.png)

<br>

Don't stress that things aren't as glowy as we all want things to be.. we'll get there.

Next, let's mask this layer as we did before.

<br>

- With the **Emissive Red** layer selected, hit the **Add mask** button and choose **Add black mask**

- Using the **Polygon fill** tool (as before), unmask areas that you wish to glow

> To stop the glowing region from reflecting light, you may wish mask your base layer.. if so:

- Select the **Iron Raw Damaged** layer and add a **white mask** - you'll see no change

- Select the **Polygon fill** tool, ensure it's set to **black** in the **PROPERTIES - POLYGON FILL** panel and mask the glowing regions - it will become more white - bear with me though

- Select the **left-hand swatch** in the **Emissive Red** layer (checker pattern) - this just gives us access again to its colour in the *PROPERTIES - FILL* panel

- Locate the **SHADER SETTINGS** panel and, in the **SHADER PARAMETERS** section, locate the **Emissive Intensity** slider

- Tweak both the **Emissive Intensity** (this panel) and the **Emissive** colour (in the *PROPERTIES - FILL* panel until you're starting to feel alright about things

<br>

![Glow no glow](https://user-images.githubusercontent.com/36719180/93168288-9a96d800-f776-11ea-9c7c-25209682a2b3.png)

<br>

FYI: I'm NOT feeling okay about things! It's not glowing! We'll solve that in the next section


<br><br>

### Camera settings

<br>

We can kind of tell that our emissive channel is working.. but there's no glow. And that's upsetting, quite frankly!

I should point out that anything we do in this section is purely to fulfil our need to see stuff glow - when we get this asset into a game engine, we'll need to harness that engine's rendering mechanics to achieve this once more. 

But gaddam it's worth it. So let's do it.

<br>

- Open the **DISPLAY SETTINGS** (top button at the top-right-hand side of the screen

- First up, let's just dip the **Environment Exposure (EV)** a little bit so we can reall see the glow

- Scroll down and locate the **CAMERA SETTINGS** section

- Check the **Activate Post Effects** checkbox

- Expand the **Glare** dropdown

- Check the **checkbox** to the right of the word **Glare** - (now we're talkin')

- Tweak the settings here - but also in conjunction with the **Emissive Intensity** (in the *SHADER SETTINGS* panel) and the **Emissive** colour (in the *PROPERTIES - FILL* panel

- You may also wish to change the *Glare* **Shape** to something like **Bloom*

<br>

![Glowy glow](https://user-images.githubusercontent.com/36719180/93168850-f0b84b00-f777-11ea-86d5-9d45edfa035e.png)

<br><br>

### Painting with alpha brushes

<br>

So far, we've only used the *Polygon fill* tool to make specific changes to our materials.

Here, we'll use alpha brushes to add more glowy bits and to apply moreintricate graphics to our landmine.

We'll start by making an emissive fill layer:

<br>

- In the **LAYERS** panel, **Add a fill layer**

- Rename it to *Emissive Green*

- In the **MATERIAL** section of the **PROPERTIES - FILL** panel, switch off all channels except **emiss**

- Still in the **MATERIAL** section of the **PROPERTIES - FILL** panel, choose an initial *green* colour to start with

- In the **LAYERS** panel, add a **black mask** to the **Emissive Green** layer - the green disappears

- In the **SHELF**, choose the **Alphas** category - we're presented with numerous black and white brushes which can be used as detail masks in a similar way to that which we've already done using the *Polygon fill* tool - except it's a brush

- Locate and select a graphic that you'd like to use on your new emissive layer - I'm going with a simple **Square Rectangle** brush for this

> Notice that the *PROPERTIES* panel now has the suffix *PAINT* and displays brush properties

> The brush is ready for use either directly on your model or in the UV Map

- Figure out where you want glowy stuff and have a go.. 

> You can adjust the brush size by holding **CTRL** + **Right mouse button** and sliding

> Also, right-clicking in the viewport briefly brings up the **BRUSH** properties

> Remember that you can 'erase' you work by inverting the brush colour (remember how masks work?) - scroll to the bottom of the **PROPERTIES** panel and locate the **GRAYSCALE** section - use the slider to adjust the brush tone

- Repeat these steps for any additional emmisive colours you wish to add

<br>

![Glow x3](https://user-images.githubusercontent.com/36719180/93170833-13e4f980-f77c-11ea-97eb-3aeabf61d129.png)

<br><br>

Now we'll do the same thing but with 'paint'

<br>

- Once again, **Add a fill layer** to the top of the **LAYER** stack

- Give the new layer a sensible name

> I'm just going to use the default white - but I'll make it whiter in the **PROPERTIES - FILL** panel

- Add a *black mask* to the layer - white disappears

- Choose another alpha brush from the **SHELF**

- Remember that holding **CTRL** + **Right mouse button** changes the brush size on the fly

> You can also rotate the brush in the **PROPERTIES** panel by using the **Angle** slider

> I'm just gonna add some little triangles on either side of the 'join' because I'm into subtly - but, by all means, go to town!

<br>

![Triangles](https://user-images.githubusercontent.com/36719180/93172189-7dfe9e00-f77e-11ea-9d3f-660bed451e23.png)

<br><br>

### Custom alphas

<br>

For the purposes of adding custom graphics, you can really easily add your own alpha brushes.

Here's how:

<br>

- Fire up **Photoshop**

- Create a new document measuring **2048px x 2048px**

- Fill the background with **black**

- Create your graphics in **white**

<br>

![Atom Can](https://user-images.githubusercontent.com/36719180/93178507-75ab6080-f788-11ea-90ed-1924b03f3c6e.png)

<br>

- Choose **File » Esport » Save for Web (legacy)**

- Use the **PNG-24** Preset and hit **Save**

- Put the file somewhere sensible and head back to **Substance Painter**

- In **Subtance**, choose **File » Import recources**

- Hit **Add resources**, locate your file and hit **Open**

- Hit the **undefined** button and set it to **alpha**

- Set the **Imprt your resources to:** field to any of those options - suggest using your 'project'

- Hit **Import**

- You'll find your custom alpha in the **SHELF** where you can use it like any other alpha brush

<br>

![Done](https://user-images.githubusercontent.com/36719180/93179305-9922db00-f789-11ea-8e67-2cd16e9004a3.png)

<br><br>

---

<br><br>

That's it for today. Tune in next time when we export our textures and maps and iset them up within both Unity and Unreal.

<br><br>

---


























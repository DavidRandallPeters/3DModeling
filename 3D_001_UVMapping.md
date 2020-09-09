# 3D Modeling for Game | 001 | UV Mapping

![Banner01](https://user-images.githubusercontent.com/36719180/90704035-7c5acb00-e2e3-11ea-9868-887cf42c25b1.png)


Notes prepared by David Peters 

---

## 001.001 | Overview

There are various methodologies used for preparing your 3D game art for use in-engine.

While the principals covered here are indeed generally applicable, we'll be taking a Maya » Substance » UE4 approach.

<br>

![Path](https://user-images.githubusercontent.com/36719180/92525813-9b140800-f278-11ea-8385-6908b4723c85.png)

<br>

The path we'll take is as follows:

- UV Mapping within Maya: You can use models of your own - or download the example 3D models provided
- Exporting these models and UVs for use within Substance Painter
- Baking high-poly data onto a low-poly model
- Applying colours and textures to your model
- Exporting from Subtance
- Importing to UE4

<br><br>

## 001.002 | What is a UV Map?

<br>

UV mapping describes the process of projecting a 2D image to a 3D model's surface for texture mapping.

In short, a UV map is a 2D representation of your 3D model - allowing textures to be mapped to your model and stored as 2D file-types - and applied to your 3D model in 3D software.

The letters **U** and **V** denote the axes of the 2D texture because *X, Y,* and *Z* are already used to denote the axes of the 3D object in digital 3D space.

<br>

![UVcoordinates](https://user-images.githubusercontent.com/36719180/92531713-f945e880-f282-11ea-9afc-ece11d7c6d81.png)

<br><br>


## 001.003 | Getting started

<br>

We'll begin in Maya. You'll need to open your Maya scene or the one I've provided you with in this repository.

The scene I've provided you with contains a simple model of some sort of proximity mine.

<br>

![Mine01](https://user-images.githubusercontent.com/36719180/92533895-9014a400-f287-11ea-8e98-b516fcfa75f5.png)

<br>

We'll do this work within Maya's UV Editor. Let's get that up and running:

- **Select** each model component in **Object Mode** (ie. Right-Click the 3D model components and choose 'Object mode' - and select all components) 
- In the main menu bar (at the very top), choose **UV » UV Editor** - this will open the UV editor

<br>

The UV editor will likely be empty.

- If for some reason it's not, in the main menu bar, choose **UV » Delete UVs** - (this will get us all on the same page)

<br>

Your editor should look something like this:

![UVEditorEmpty](https://user-images.githubusercontent.com/36719180/92534808-e1be2e00-f289-11ea-9eed-4a526fe64cc6.png)

<br>

Maya's UV Toolkit contains a wide range of handy tools for this sort of work, so let's get that open, too:

- In the **UV Editor**'s menu bar, choose **Tools » Show UV Toolkit**
- I like to dock this beneath my *Channel Box* and *Attribute Editor* - by all means, do the same

<br>

We need some information to work with - so we'll generate some initial UV data that we'll then adjust to suit our needs.

<br>

- With your model components still selected, hit **Planar** in the **UV Toolkit** - you'll find this in the **Create** section

<br>

![Initial UV map](https://user-images.githubusercontent.com/36719180/92536405-bc332380-f28d-11ea-9f29-db864a091cb4.png)

<br>

We now have some data to begin working with.

Note that Maya has filled up all available real-estate within the UV grid's first quadrant (known as a *U-Dimension* or *U-DIM*).

That is to say that all available space - from 0.0, 0.0 (bottom-left) to 1.0, 1.0 (top-right) has been utilised. 

It is within *this* space that our *UV Shells* must ultimately be positioned in order for them to be included in the map. 

We'll talk more about this soon.

<br><br>


## 001.004 | Applying a default checker [optional]

<br>

It's worthwhile working with a checker guide so that you can track the distortion of the 2D map in the UV editor.

Maya provides a checker pattern by default. You can follow these steps to apply it - however, we'll shortly apply our own, as Maya's one is a little hard on the eyes.

So, you can skip these steps and go directly to *Applying a custom checker.*

<br>

Optional:

- With the model components still selected, hit the **Checker Map** button in the **UV Editor** (top-right)

![Checker Map](https://user-images.githubusercontent.com/36719180/92537657-c7d41980-f290-11ea-84a1-3bba063d1f72.png)

<br>

You should now see a checker grid projected onto your model like this:

<br>

![Default checker](https://user-images.githubusercontent.com/36719180/92537915-71b3a600-f291-11ea-8f81-c856a47638fc.png)

<br><br>


## 001.005 | Applying a custom checker

<br>

![UVChecker](https://user-images.githubusercontent.com/36719180/92535067-7f196200-f28a-11ea-909b-b7b3a1f11f36.png)

<br>

The image you see here is easier on the eyes and just lends itself a little better to the task at hand.

By applying this checker to our model, we'll simultaneously learn how to apply a texture to a model in Maya (if this isn't a skill you already have).

<br>

- Download the above checker image to a folder called **images** within your Maya scene folder - if you're using the provided Maya scene, the folder will have the extension: *3DAssetPipeline » images*
- In Maya, open the **Hypershade window** - the easiest way to do this is via the 'teal shader' button in the main toolbar (top) it looks like this:

![Hypershade](https://user-images.githubusercontent.com/36719180/92539920-1b496600-f297-11ea-9ba4-63d731f97e5c.png)

<br>

- In the **Create** panel within the *Hypershade* window, choose **Arnold » Shader » Surface » aiStandardSurface** 
> This creates a new shader that we'll use to apply textures with

<br>

- In the **Property Editor** panel within the *Hypershade* window, give the material a name: *aiCheckerPattern*
> This goes in the aiStandardSurface field

> Adding the ai prefix ('ai', signifying Arnold materials) is a general good habit to get into. It helps us identify the types of materials we've created, at a glance

<br>

- In the **Base** section of the **Property Editor** panel, locate **Color** and click the checkered icon to its right:

<br>

![Base Color](https://user-images.githubusercontent.com/36719180/92541777-1981a180-f29b-11ea-941b-2251c534255c.png)

<br>

- From the list that pops up, choose **File**
- In the **Property Editor** panel, hit the folder icon next to **Image Name**
- Locate the checker pattern that you downloaded just now - it should be in your project folder's **images** folder - and choose it

<br>

![Material File Attributes](https://user-images.githubusercontent.com/36719180/92542071-e986ce00-f29b-11ea-8762-53185d94a6d9.png)

<br>

- Close the **Hypershade Window**
- Ensure all components are selected in the main viewport
- **Right-click** and hold (with the cursor above an object in the viewport) and choose **Assign Existing Material » aiCheckerPattern

<br>

![Checker applied](https://user-images.githubusercontent.com/36719180/92542439-e0e2c780-f29c-11ea-9562-6fae738bad1c.png)

<br>

We now have an ideal texture applied to our model components for the purpose of UV mapping.

As you orbit your model, you'll almost certainly see distrotion of the checker grid we've just added. This is exactly what *a)* we're looking for and *b)* will seek to solve in the following steps.

<br>

>If you don't see the texture applied to your model, make sure you have **Textured** switched on in the viewport toolbar:

![Textured](https://user-images.githubusercontent.com/36719180/92542619-58185b80-f29d-11ea-954c-6b8cc16d96d7.png)

<br>

If you wish, you can adjust the way this texture is applied to your model via the *Attribute Editor*:

- Select the **aiCheckerPattern** tab at the top of the **Attribute Editor**
- Hit the arrow-lookin' icon to the right of the **Color** field in the **Base** section
- Select the **place2dTexture** tab 

In this section, you may wish to alter the **Repeat UV** parameters to, say, *5.000 x 5.000*.

<br>

>A final note: if your texture is blurred, either in the viewport or the UV Editor, try saving your project and restarting Maya. Textures should come right when you reopen the project.

<br><br>


## 001.006 | Cutting and Sewing

<br>

Now, we'll make a start using the tools that will allow us to make a neat UV map for our model.

<br>

- Make the checker texture invisible for a moment by switching off **Textured** in the main viewport.

<br>

![Textured](https://user-images.githubusercontent.com/36719180/92542619-58185b80-f29d-11ea-954c-6b8cc16d96d7.png)

<br><br>

### Cutting seams

<br>

- In **Edge** select mode, select any edge (or edges) in your model
- Open your **UV Toolkit** - should be docked under your *Attribute Editor* etc. If you've lost it somehow, you can reopen it via the *UV Editor* under *Tools » Show UV Toolkit*
- In the **UV Toolkit**, expand **Cut and Sew**
- Hit **Cut** to create a seam

If you deselect everything, you'll now see a bold white line where you just made a seam. 

If you were to make an entire cut (such as an edge loop) that disects your model, you'd now have two *UV Shells* - whereas, before, you just had the one. More on those shortly.

Notice that the seam is reflected both in the viewport and in the UV Editor.

>You can hit the **Display Image** button in the *UV Editor* to hide the checkers.

<br>

![Seam / cut](https://user-images.githubusercontent.com/36719180/92546409-8ea6a400-f2a6-11ea-972e-096d110ceb4b.png)

<br>

- By **Right-clicking** in the UV editor (and holding) and choosing **UV Shell**, you can select separate regions of your UV map
- By using the usual **Move** tool, you can reposition those regions

<br>

![UV Shell](https://user-images.githubusercontent.com/36719180/92547336-c57db980-f2a8-11ea-990d-e33a3dd97ef2.png)

<br>

- In the main viewport, hit **Textured** once more to show the checkers
- In the **UV Editor**, move UV Shells around and observe what happens in the main viewport to get a feel for what's going on

<br><br>

### Sewing seams

<br>

- By reselecting any edges that you just cut, and hitting **Sew** in the **UV Toolkit**, you can merge UV Shells back together

Note that, if you've moved Shells away from each other and you then sew, it bridges the gap between the two - irrespective of position. This can mean that regions in the UV editor can become distorted. To avoid this, you can alternately use **Stitch Together** (also in the *Cut and Sew* section of the *UV Toolkit*)

I suggest you give that a try now to observe its effects.

<br><br>

### Rule of thumb

<br>

As a general rule, when establishing where to put a seam and subsequently making cuts, you want to put as few cuts and seams in important areas as possible. 

Important areas are likely to be regions of your model that will be seen the most - or areas that have no natural edges or corners (eg. the middle of a large surface).

Simply put:

<br>

**You should attempt to hide your seams wherever practical.**

<br>

This is for two main reaons:

1. Seams can become visible when applying textures - though, this is becoming less and less and issue as software such as Substance Painter becomes more intuitive and versatile.

2. In a production environment, someone else will likely be creating textures for UV maps that you've created. You therefore want to make it as clear as possible what's what and generally make their job easier.

<br><br>


## 001.006 | The objective

<br>

We're essentially trying to achieve the following:

<br>

- Establish the neatest, cleanest way of unfolding our 3D model
- Position its shell (or shells) in a way that optimises use of that 1x1 UV quadrant (*U-DIM*) mentioned earlier - as wasted space is tantamount to wasted resolution and ultimately wasted resources in-engine
- Doing these things in a way that results in zero texture distortion

<br><br>


## 001.007 | Alternate projection methods

<br>

The best way to get comfortable with this process is to try it out - which we'll do very shortly.

But first, a couple more tips and tricks to help you along your way.

The projection method we initially used to generate our UV information is an okay starting point, but our task will prove slightly easier if we just take a little more care when generating that initial data.

<br>

- At this point, I *do* suggest you watch this video by FlippedNormals. They cover a range of concepts that are best seen demonstrated.
[UV Mapping - complete basics](https://www.youtube.com/watch?v=dj0uXid9oGo&t=476s&ab_channel=FlippedNormals)

<br>

Meanwhile, I'll demonstrate what I think is the best starting point for this landmine model.

We'll start with the 'cap' object. Ultimately, I'll make this a glowing light that will indicate to the player that the device is armed and dangerous.

I'm going to isolate the object from the body of the mine to make things clearer.

<br>

- In the main viewport, in **Object mode**, select just the 'cap' object
- Hit **Ctrl+1** to isolate it
- With the 'cap' object still selected, in the **UV Toolkit**, hit **Best Plane** - this will prompt a dialogue:

<br>

![Dialogue](https://user-images.githubusercontent.com/36719180/92551669-ad129c80-f2b2-11ea-96c3-4612a458b55c.png)

<br>


- The most prominent surface on this object is its top-most [circular] region. So we should choose a pie-slice from that region to determine the projection plane.

<br>

![Pie slice](https://user-images.githubusercontent.com/36719180/92552047-d122ad80-f2b3-11ea-8a30-116901262b0e.png)

<br>

- Once you've selected a triangular segment within that top-most region, hit **Enter** 

<br>

![New projection](https://user-images.githubusercontent.com/36719180/92552128-0a5b1d80-f2b4-11ea-904d-c56134aa37bd.png)

<br>

We now have a new projection that occupies the entire UV quadrant.

But we still have faces that are hidden beneath that outer-most rim.. We need to make slices that allow those faces to fold 90° upward, as it were..

<br>

- In **Edge** mode, select the edges that need cutting in order to make that fold..

![Fresh cuts](https://user-images.githubusercontent.com/36719180/92552821-9d488780-f2b5-11ea-8e62-b530c0dfc667.png)

- When you're satisfied that you've found the most logical approach, hit **Cut** in the **UV Toolkit**

<br>

The cuts are now made.. next; we'll unfold those faces so that all faces can be seen in one top-down projection.

<br><br>


## 001.008 | Unfolding

<br>

To demonstrate this, I'll continue with the 'cap' object from the previous section.

Now that we've made those cuts, it should be ready to unfold.

<br>

- In the **UV Toolkit**, expand the **Unfold** section
- With the 'cap' object still selected, hit **Unfold**

<br>

![Cap unfolded](https://user-images.githubusercontent.com/36719180/92552979-fa443d80-f2b5-11ea-9d96-36767934e49f.png)

<br>

You can see in this image that the checker texture has issues.. the pattern doesn't line up as we'd want it to.

That's okay! This particular workflow doesn't really care about that right now - Substance Painter will take care of that for us.

The main thing, right now, is that there's no distortion or stretching of the texture - which there's not.

This is a good projection.

<br>

- To make the rest of your model visable again (having isolated the cap) simply hit **Ctrl+1** again

<br>

So. That's the majority of the workflow covered. There's still a little more to it. For example, there are optimisation tools that we'll look at and we need to pack our entire map inside this first U-DIM.

For now, I'll briefly demonstrate my approach to the rest of this landmine model - then we'll wrap it up and export.

<br><br>


## 001.009 | Finishing the map contents

<br>

This section simply repeats previous steps in order to get the rest of the model mapped.

<br>

- First of all, I'm setting the *Smooth Preview mode* to **1** (ie. not smoothed) - this way I can more easily find my intended joins in the object
- Here's a quick colour-coding exercise to indicate where I think various textures will go when we get to Substance Painter:

<br>

![ColourCode](https://user-images.githubusercontent.com/36719180/92558412-92e0ba80-f2c2-11ea-9f58-f510cd1bcdcc.png)

<br>

>It's not too late to make tweaks to the model - so I might do that now..

- When you're all set, isolate the object (**Ctrl+1**)

>I'm going to make the yellow separate to [what will be] the metal.. so:

- Make seams where those colours meet. This will just make things simpler in Substance.

> This object is now split into four *UV Shells*

<br>

![Four shells](https://user-images.githubusercontent.com/36719180/92559249-4dbd8800-f2c4-11ea-88f2-1ddeb16a9f57.png)

<br>

- I'll now re-project the two 'metal' shells and the yellow 'lid' using **Best Plane** in the same way as we did before - although, I've just realised that the inside lip (that goes downwards, inside the top) will overlap itself - so I'm cutting that off. We now have five *UV Shells* making up this object.

<br>

![FiveShells](https://user-images.githubusercontent.com/36719180/92568972-0fc86000-f2d4-11ea-9d12-51143c109635.png)

<br>

- I made the decision to snip those yellow bands into ribbons. So we now have seven *UV Shells* making up this object.

<br>

![Seven Shells](https://user-images.githubusercontent.com/36719180/92572450-91ba8800-f2d8-11ea-9bea-566e5071c5f6.png)

<br><br>

So I'm now satisfied that all *UV Shells* have been created and unfolded ina way that allows direct projection of a texture map onto all faces.

We just have a few final steps to take before this UV map will be ready for export.

<br><br>


## 001.010 | Optimisation

<br>

The UV Shells that we've created are pretty good.. we could just scale these down so that they fit within the U-DIM and export.

But all will not be perfect.

The process we've just undergone can be thought of as broad strokes. In most cases, there will be slight inconsistencies that may or may not result in dodgy texture projection. 

For example, take a close look at the fins on the 'Before' image below. They're not quite right.

<br>

![Optimise before/after](https://user-images.githubusercontent.com/36719180/92574621-6edda300-f2db-11ea-92a1-7dfec21e5ddd.png)

<br>

- Select the *UV Shell* in question and hit **Optimize** in the **UV Toolkit** - the result is shown above in the 'After' image

<br>

This is an improvement but, in this case, it didn't make a whole heap of difference. So I defer now to the *Optimize Tool*

<br>

- Choose the **Optimize Tool** in the **UV Toolkit** 

> This is something like a Photoshop brush. To use it, you click and 'paint' over areas that you think need further optimisation.

<br>

- Brush around the *UV Shell* until you stop noticing any further change to the Shell's shape

<br>

![Optimize Tool](https://user-images.githubusercontent.com/36719180/92574851-c0862d80-f2db-11ea-8547-7667ae2c75e4.png)

<br>

The result is pictured above. This is pretty much perfect.

<br>

- Repeat these optimisation steps for all *UV Shells*

<br><br>


## 001.011 | Packing

<br>



















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

Note that Maya has filled up all available real-estate within the UV grid's first quadrant.

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

- gdsg










# 3D Modeling for Game | 002 | Substance


![Banner](https://user-images.githubusercontent.com/36719180/90928812-ad560f80-e44b-11ea-8bc2-cf44378c8e36.png)


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
3. Fire up Substance and import low-poly model
4. Bake all maps using the high-poly model as a source
5. Apply materials
6. Add an emissive channel for glowing stuff
7. Add custom graphics in Photoshop

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
- Make the **High-poly** layer visible and also delete that mesh's history
- Make that layer invisible again

<br><br>

### Common pivots

This next bit isn't for the benfit of Substance but for your chosen game engine (in this case, Unreal).

This is a good habit to get into for two reasons:

> 1. For the purpose of assembling complex models (with multiple components) quickly, in-engine. <br> <br> Imagine you have a table asset that has a bunch of beer mugs and swords on it (let's assume that these can't be picked up - this approach will oftentimes be irrelevant for collectible items as they would typically want a centered pivot). These mugs and swords are bound to be separate components (and ultimately separate 3D assets) - not least because the contents of the table may vary from scene to scene (or from table to table). <br> <br> To assist with rapid assembly in-engine, we can establish common pivot points for all items, here in Maya - meaning that we can literally drag and drop each varied (and variable) asset and they'll assemble perfectly without fiddly manipulation. Table/item combinations can then be saved as varied Prefabs (Unity) or Blueprints (Unreal).

<br>

> 2. So that when objects are placed or instantiated in-engine, they'll instantiate *above* the ground-plane - not in the middle of it.

<br><br>

So. Let's get this skill down:

<br>

- Hit **Space** and choose one of the side orthographic projections
- Select the object, hit **W** (move) and notice that its pivot is currently centered
- Hit **D** - the gizmo changes its appearance - we are now able to move that pivot









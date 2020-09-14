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

## 002.002 | High-poly model

<br>

I'll continue using the landmine model from last time.

For the purposes of this tutorial, I suggest you do the same - *regardless of whether or not you have your own model to work with.*

Once you have the basics down, you can go back and try it out with your own model.

I've provided a new Maya scene that contains both high-poly and low-poly iterations of the landmine.

<br>

- Download the new scene now and open it in Maya
- Ensure that the **Channel Box/Layer Editor** tab is active

<br><br>

You're presented with the *high-poly* version of the landmine model.

<br>

![High-poly landmine](https://user-images.githubusercontent.com/36719180/93149242-f0a15680-f749-11ea-970a-69d353621a57.png)

<br>

- Select the model and explore its detail - there's a dent in the shell, joins and depressions
- Open the UV Editor and notice that it's a mess in there! This is fine. We're only interested in the low-poly model's UV map
- In the **Layers** section (at the bottom of the **Channel Box/Layer Editor**), hit the **V** to the right of **HighPoly** layer to make that layer and its contents invisible
- Do the inverse for the **LowPoly** layer - making it visible
- Notice that the low-poly and high-poly meshes share the exact same world-space - *this is important for accurate projection!*








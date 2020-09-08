# 3D Modeling for Game | 001 | 3D Game Art Pipeline via Substance

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

## 001.002 | UV Mapping in Maya

<br>

### What is a UV Map?

UV mapping describes the process of projecting a 2D image to a 3D model's surface for texture mapping.

In short, a UV map is a 2D representation of your 3D model - allowing textures to be mapped to your model and stored as 2D file-types - and applied to your 3D model in 3D software.

The letters **U** and **V** denote the axes of the 2D texture because *X, Y,* and *Z* are already used to denote the axes of the 3D object in digital 3D space.

<br>

![UVcoordinates](https://user-images.githubusercontent.com/36719180/92531713-f945e880-f282-11ea-9afc-ece11d7c6d81.png)

<br><br>

### Getting started

We'll begin in Maya. You'll need to open your Maya scene or the one I've provided you with in this repository.

The scene I've provided you with contains a simple model of some sort of proximity mine.

<br>

![Mine01](https://user-images.githubusercontent.com/36719180/92533895-9014a400-f287-11ea-8e98-b516fcfa75f5.png)

<br>

We'll do this work within Maya's UV Editor. Let's get that up and running:

- Select each model component in 'Object Mode' (ie. Right-Click the 3D model and choose 'Object mode') 
- In the main menu bar (at the very top), choose **UV » UV Editor** - this will open the UV editor

<br>

The UV editor will likely be empty.

- If for some reason it's not, in the main menu bar, choose **UV » Delete UVs** - (this will get us all on the same page)

<br>

Your editor should look something like this:

![UVEditorEmpty](https://user-images.githubusercontent.com/36719180/92534808-e1be2e00-f289-11ea-9eed-4a526fe64cc6.png)

<br>

It's worthwhile working with a checker guide so that you can track the distortion of the 2D map in the UV editor.

Maya provides a checker pattern by default. You can follow these steps to apply it - however, we'll shortly apply our own, as Maya's one is a little hard on the eyes - so you can skip this step and go straight to the next one.

<br>



<br><br>

### Applying a custom checker

![UVChecker](https://user-images.githubusercontent.com/36719180/92535067-7f196200-f28a-11ea-909b-b7b3a1f11f36.png)








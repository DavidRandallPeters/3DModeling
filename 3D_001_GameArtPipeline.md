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

The letters **U** and **V** denote the axes of the 2D texture because *X, Y,* and *Z* are already used to denote the axes of the 3D object in model space.

<br>

![UVcoordinates](https://user-images.githubusercontent.com/36719180/92531713-f945e880-f282-11ea-9afc-ece11d7c6d81.png)

<br><br>

### Getting started

We'll begin in Maya. You'll need to open your Maya scene or the one I've provided you with in this repository.

The scene I've provided you with contains a simple model of some sort of proximity mine.

<br>

![Mine01](https://user-images.githubusercontent.com/36719180/92533895-9014a400-f287-11ea-8e98-b516fcfa75f5.png)

<br>









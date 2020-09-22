# 3D Modeling for Game | 003 | Substance » Unity


![Banner](https://user-images.githubusercontent.com/36719180/93857076-23c98400-fd0e-11ea-9326-9f75bfd71de5.png)


Notes prepared by David Peters

Using Substance Painter 2020.2.1 (6.2.1) + Unity 2020.1.6f1

---

## 003.001 | Exporting from Substance Painter

<br>

We'll start from where we left off in *3D_002_Substance.md*.

I'll assume you're happy with your model's paint job and are about ready to send it over to Unity.

I'll include an extra [optional] step that involves opening your *BaseMaterial* texture in Photoshop to make graphical additions there.

Let's get into it:

<br>

- Open your *Substance Painter* project
- In the main menu, choose **File » Export Textures** (or just hit **Ctrl + Shift + E**)
> We set up this project using the Unreal template - but now's our chance to change that
- Ensure that **Output Template** is set to **Unity**
- Double-check **Output directory** to make sure your destination folder is sensible
- **8-bit .png** is fine
- Set size to something sensible - **2048** is probably fine
> If either your model is 'physically' very large in your scene or you've included a LOT of model components, you may want to increase this to 4k .. but that's unlikely.. and expensive.. Remember that we're not just exporting a base material but three other maps also - it all adds up. So maybe just see how you go with 2k and redo the export if you need to.
> *Padding* is the same as 'bleed' (in printing terms). It spreads the colour information outside of your UV regions/shells to mitigate against seam-lines.
- Check that **Padding** is set to **Dilation infinite**
- Hit **Export**

<br>

![Substance export settings](https://user-images.githubusercontent.com/36719180/93857430-ab16f780-fd0e-11ea-8783-eefa6974b760.png)

<br>

Substance will run the export. You'll notice that the file-names have inherited the name of your Maya shader - most likely this is *lambert1*.

<br>

![Lamberts](https://user-images.githubusercontent.com/36719180/93857532-d699e200-fd0e-11ea-8fc5-b087e8c2d1c7.png)

<br>

By all means leave this as is - I'm kinda fussy though - so I'll open the destination folder and tidy up those file names.

---

## 003.002 | Importing to Unity

<br>

- Fire up your Unity project - or create one for the occasion.

>This tutorial covers Unity's *Universal Render Pipeline (URP)* - if for some reason you'd like to use the *HDRP* for your project, let me know and I'll generate additional steps for *HDRP*.

- In a sensible location in the **Project** browser, create a folder called **Landmine**

> This will contain all the relevant textures, materials and mesh for this asset.

- Create a **Materials** folder, a **Textures** folder and a **Mesh** folder

- Open the **Textures** folder

- **Right-Click** inside that folder and choose **Import New Asset**

- Locate and import your textures

<br>

![Textures imported](https://user-images.githubusercontent.com/36719180/93858445-49578d00-fd10-11ea-8a38-f0504383766b.png)

<br><br>

---

## 003.003 | Material set-up

<br>

- In the **Textures** folder, select the **Normal map**

- In the **Inspector**, set the **Texture Type** to **Normal map**

- Hit **Apply** at the bottom of the **Inspector**

- Go into your **Mesh** folder and import your **low-poly mesh** - the one you imported into Substance Painter

- Drag the model into your scene - it'll likely look something like this:

<br>

![Mesh imported](https://user-images.githubusercontent.com/36719180/93864628-4a40ec80-fd19-11ea-92de-ba85b4b596ec.png)

<br>

- Go into your **Landmine » Materials** folder

- **Right-click** inside the folder and choose **Create » Material**

- Call it **LandmineMat**

- Drag the new material from the **Project Browser** onto the landmine object in the scene

- With the material still selected in the **Project Browser**, look at the top of the **Inspector** for the **Shader** dropdown

- Set this to **Standard (Specular setup)**

- Hit the 'circle selector' (that's what Unity calls the tiny little button to the left of the word **Albedo**) to open the *Select Texture* window for **Albedo**

- Locate and select the **Landmine_AlbedoTransparency** texture and close the window - your landmine should now have a paint-job

<br>

![Paint job](https://user-images.githubusercontent.com/36719180/93869688-3e0c5d80-fd20-11ea-83cb-ad7ce6795904.png)

<br>

- 






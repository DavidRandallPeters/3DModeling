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

![Mesh imported](https://user-images.githubusercontent.com/36719180/93870949-08687400-fd22-11ea-9501-484cc297cf27.png)

<br>

- Go into your **Landmine » Materials** folder

- **Right-click** inside the folder and choose **Create » Material**

- Call it *LandmineMat*

- Drag the new material from the **Project Browser** onto the landmine object in the scene

- With the material still selected in the **Project Browser**, look at the top of the **Inspector** for the **Shader** dropdown

- Set this to **Standard (Specular setup)**

- Hit the 'circle selector' (that's what Unity calls the tiny little button to the left of the word **Albedo**) to open the *Select Texture* window for **Albedo**

- Locate and select the **Landmine_AlbedoTransparency** texture and close the window - your landmine should now have a paint-job

<br>

![Paint job](https://user-images.githubusercontent.com/36719180/93871217-6301d000-fd22-11ea-8b9a-36cf40ab6119.png)

<br>

- In the same way, connect the **SpecularSmoothness** map to the material's **Specular** channel

<br>

![Specular added](https://user-images.githubusercontent.com/36719180/93871797-503bcb00-fd23-11ea-82d7-ffad0e5b289b.png)

<br>

- Connect the **LandmineNormal** map to the **NormapMap** channel

<br>

![Normal added](https://user-images.githubusercontent.com/36719180/93872012-a872cd00-fd23-11ea-87d4-41224c04f07d.png)

<br>

- Check the **Emission** checkbox

- Connect the **LandmineEmission** map to the **Emission » Color** channel

<br>

![Emission added](https://user-images.githubusercontent.com/36719180/93872780-c68cfd00-fd24-11ea-80f8-114ecb9b5699.png)

<br><br>

That's the material all set up. But our emission isn't glowing as we'd probably like it to.

<br><br>

---

## 003.004 | Adding Post-processing

<br>

In order for our emissive materials to glow nicely, we need to set up Unity's post-processing stack.

This is a package that we need to import from the cloud.

<br>

- In the top menu bar, choose **Window » Package Manager**

- Check that the **Packages** list's filter (top-left) is set to **Unity Registry** - NOT *In Project* or *My Assets* - this will allow the list to be populated fully

- Search the list for **Universal Render Pipeline** and **Install** it

> This package can now be found in the **Packages** folder in the **Content Browser**

- In the **Content Browser**, navigate to **Packages » Post Processing » Postprocessing » Runtime**

<br>

![Post Process folder](https://user-images.githubusercontent.com/36719180/93874331-503dca00-fd27-11ea-8e4c-4032c1f01677.png)

<br>

- From the open folder in the **Project Browser**, drag **PostProcessLayer** out and onto the **Main Camera** in your **Hierarchy** to attach it

- Also drag **PostProcessVolume** onto the **Main Camera** to attach that

- Select the **Main Camera** in the **Hierarchy**

- At the top of the **Inspector**, use the **Layer** dropdown to **Add layer...**

- In any free slot (slot #8 is probably free), add a layer called *PostProcessing*

<br>

![New layer](https://user-images.githubusercontent.com/36719180/93876230-97798a00-fd2a-11ea-981a-5e88459974df.png)

<br>

- Reselect the **Main Camera**

- Ensure that its **Layer** is set to **PostProcessing**

<br>

![Post Processing layer](https://user-images.githubusercontent.com/36719180/93876271-aeb87780-fd2a-11ea-880f-c5f77e15b61b.png)

<br>

- 











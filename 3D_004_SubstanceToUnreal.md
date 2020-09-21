# 3D Modeling for Game | 004 | Substance » Unreal

![Banner Unreal](https://user-images.githubusercontent.com/36719180/93731545-91e44d00-fc21-11ea-8de9-4594e1a276f8.png)


Notes prepared by David Peters

Using Substance Painter 2020.2.1 (6.2.1) + Unreal 4.23.1

---

## 004.001 | Exporting from Substance Painter

<br>

We'll start from where we left off in *3D_002_Substance.md*.

I'll assume you're happy with your model's paintjob and are about ready to send it over to Unreal.

I'll include an extra [optional] step that involves opening your *BaseMaterial* texture in Photoshop to make graphical additions there.

Let's get into it:

<br>

- Open your *Substance Painter* project
- In the main menu, choose **File » Export Textures** (or just hit **Ctrl + Shift + E**)
> We set up this project using the Unreal template - if you didn't, now's your chance to change that
- Ensure that **Output Template** is set to **Unreal Engine 4 (Packed)**
- Double-check **Output directory** to make sure your destination folder is sensible
- **8-bit .png** is fine
- Set size to something sensible - **2048** is probably fine
> If either your model is physically very large in your scene or you've included a LOT of model components, you may want to increase this to 4k .. but that's unlikely.. and expensive.. Remember that we're not just exporting a base materai but three other maps also. It all adds up. So maybe just see how you go with 2k and redo the export if you need to.
> *Padding* is the same as 'bleed' (in printing terms). It spreads the colour information outside of your UV regions/shells to mitigate against seam-lines.
- Check that **Padding** is set to **Dilation infinite**
- Hit **Export**

<br>

![Export settings](https://user-images.githubusercontent.com/36719180/93734536-b9411700-fc2d-11ea-808e-70088bbda8a1.png)

<br>

Substance will run the export. You'll notice that the file-names have inherited the name of your Maya shader - most likely this is *lambert1*.

<br>

![Lambert](https://user-images.githubusercontent.com/36719180/93734710-80557200-fc2e-11ea-818c-2e3fcdc822f1.png)

<br>

By all means leave this as is - I'm kinda fussy though - so I'll open the destination folder and tidy up those file names.

<br><br>

---

## 004.002 | Importing to Unreal

<br>

- Fire up your Unreal project (or create one for the occasion)
- In the **Content Browser**, creat a folder for the asset - I'm calling mine *Landmine*
> This will contain all the relevant textures, materials and mesh for this asset.
- Create a **Materials** folder, **Textures** folder and **Mesh** folder
- Open the **Textures**
- Hit the **Import** button at the top of the **Content** browser
- Locate and import your textures

<br>

![Import](https://user-images.githubusercontent.com/36719180/93734835-0376c800-fc2f-11ea-9cb1-07328d8c1cc9.png)

<br>

- In the **Content Browser** Double-click the **OcclusionRoughnessMetallic** file to open the asset
- In the **Texture** sections of the **Details** panel, *uncheck* the **sRGB** checkbox
- Hit **Save** (top-left) and close the window

> The comparison below shows the final asset with and without sRGB. Textures created in Substance seem to prefer not to be treated with sRGB.

<br>

![sRGB Comparison](https://user-images.githubusercontent.com/36719180/93735703-f14a5900-fc31-11ea-98b0-b6a0514a3e1a.png)

<br>

- Go into your **Landmine » Mesh** folder and import your **low-poly mesh** - the one you imported into *Substance Painter*
- Drag the model into your scene - it'll likely look something like this:

<br>

![Mesh import](https://user-images.githubusercontent.com/36719180/93735988-ec39d980-fc32-11ea-91c4-1ebbcc3e31b8.png)

<br>

- Go into your **Landmine » Materials** folder
- **Right-click** inside that [empty] folder and choose **Material** to create a new material
- Name it **LandmineMat**
- Double-click the new material to open it in Unreal's *Material editor*

> You'll see a material node with empty slots - it's our task to plug our textures into the correct slots to make this render as it we want it to

<br>

![Empty material slots](https://user-images.githubusercontent.com/36719180/93738003-c9122880-fc38-11ea-83db-d5847e52aab6.png)

<br>

- **Right-click** in empty graph space (to the left of the material node) 
- Start typing **TextureSample** in the search field and choose that when it becomes available
- Locate the **Material Expression Texture Base** section of the **Details** panel
- Use the drop-down next to the **Texture** swatch to locate your **Landmine_BaseColor** texture asset and choose it
- In the graph, drag off the **Texture Sample** node's **RGB** pin and connect it to the **Base Color** pin in the **New Material** node

<br>

![BaseColor](https://user-images.githubusercontent.com/36719180/93738658-6faaf900-fc3a-11ea-8f11-3aa067c8004c.png)

<br>

- 






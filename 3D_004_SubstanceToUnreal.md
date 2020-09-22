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
> If either your model is physically very large in your scene or you've included a LOT of model components, you may want to increase this to 4k .. but that's unlikely.. and expensive.. Remember that we're not just exporting a base material but three other maps also - it all adds up. So maybe just see how you go with 2k and redo the export if you need to.
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
- Open the **Textures** folder
- Hit the **Import** button at the top of the **Content** browser
- Locate and import your textures

<br>

![Import](https://user-images.githubusercontent.com/36719180/93734835-0376c800-fc2f-11ea-9cb1-07328d8c1cc9.png)

<br><br>

---

## 004.003 | Material set-up

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
- Select the **Landmine** in your scene
- Drag the **LandmineMat** material from the **Content Browser** into the **Element 0** slot in the **Materials** section of the **Details** panel to apply this material to the Actor

<br>

![Blank material](https://user-images.githubusercontent.com/36719180/93833175-fd82f480-fccb-11ea-8b3f-23005f675020.png)

<br>

- Double-click the **LandmineMat** material in the **Content Browsert** to open it in Unreal's *Material editor*

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

- Select the **Texture Sample** node and hit **CTRL + W** to duplicate it three times - you should four when you're done
- Load your remaining three textures in the other **Texture Sample** nodes as we've just done, as indicated below:

<br>

![Plug 'em in](https://user-images.githubusercontent.com/36719180/93739126-a3d2e980-fc3b-11ea-9ce7-1e5674d174b8.png)

<br>

> The three colour channels (RGB) in our **OcclusionRoughnessMetallic** texture correspond to material properties as follows:

> **R** » **Ambient Occlusion (AO)**

> **G** » **Roughness**

> **B** » **Metallic**

<br>

- Connect those channels accordingly

<br>

![OcclusionRoughnessMetallic](https://user-images.githubusercontent.com/36719180/93740156-0c22ca80-fc3e-11ea-8689-d380235a3709.png)

<br>

- Connect the **RGB** channel of the **Normal** map to **Normal**

<br>

> Emission is a little different.. we need to indicate how strongly to emit. We do this by multiplying the colour values in the texture by a number that we'll provide.

- Right-click in empty graph space and search for **Multiply** and choose it

- Connect the **Emmissive** texture node's **RGB** pin to the **A** input of the **Multiply** node

- Hold the number **1** key and **left-click** in empty graph space to create a **Constant** node

- Connect the **Constant** node to the **B** input of the **Multiply** node

- Connect the **Multiply** node to the **Emissive Color** channel

> You won't see any change in the preview just yet - we need to provide a constant value

- Select the **Constant** node

- In the **Details** panel, provide a *Material Expression Constant* **Value** of about **40** - you can come back and change this later to adjust emission if you feel the need

<br>

![Material setup complete](https://user-images.githubusercontent.com/36719180/93741538-bc91ce00-fc40-11ea-9b64-fd2c64be28ba.png)

<br>

- That's all we need to do in here - hit **Save** in the top-left of the screen and head back to the editor

<br>

![Glow, no glow](https://user-images.githubusercontent.com/36719180/93834808-412c2d00-fcd1-11ea-84e9-c9f9bc0158f2.png)

<br>

The landmine in your scene should be starting to look pretty good - but it may not be glowing quite as you'd expect..

<br><br>

---

## 004.004 | Applying post-processing effects

<br>

To make our emissive regions really *glow,* we need to utilise UE4's post-processing effects.

To do this, we simply need to include a *Post Process Volume* in our scene

This is fairly straightforward:

<br>

- Locate the **Place Actor** panel (also known as the **Modes** panel) - this is usually docked to the left of the viewport but can otherwise be accessed via **Window » Editor Modes » Modes panel / Place Actor** 

- Select the **Visual Effects** category

- Drag a **Post Process Volume** into the scene - this is a cube / volume that applies your chosen visual effects while the camera is *within* that volume

- Scale the volume to encompass your scene

- With the **Post Process Volume** selected, locate the **Lens** section in the **Details** panel

- Expand **Bloom**

- Check the **Method**, **Intensity** and **Threshold** checkboxes

- Ensuring that the editor's camera is inside the **Post Process Volume**, experiment with these values until you achieve the look you're going for

> While you're here, experiment with the other lens effects in this section.

<br><br>

![Hero shot](https://user-images.githubusercontent.com/36719180/93834350-b3037700-fccf-11ea-955b-d57c12707aea.png)

<br><br>

---

## 004.005 | Adding detail in Photoshop [optional]

<br>

Substance Painter isn't without its limitations.. If you're comfortable using Photoshop, this section will come as a handy option for adding detail to your base texture that you couldn't quite nail in Substance Painter.

<br>

- Locate your *pre-Unreal / post-Substance* **Landmine_BaseColor** texture asset in Windows Explorer / Mac Finder
- Open it in **Photoshop**

<br>

![Open texture in Photoshop](https://user-images.githubusercontent.com/36719180/93837681-35456880-fcdb-11ea-8a0e-464b270dd321.png)

<br>

Here, we can add whatever details we like, save it and reimport the asset to Unreal.. But how do we colour within the lines, as it were? We don't have our UV map here in Photoshopto guide us..

Let's hop into our Maya project and retrieve that UV Map.

<br>

- Open your asset scene in Maya
- Open the **UV Editor**
- Hit the little camera **UV Snapshot** button - it looks like a camera
- Choose a sensible destination for the snapshot
- Set the **Image Format** to **PNG** so that there's an alpha channel (transparency)
- Ensure the resolution matches the texture resolution that you chose when you exported the textures from Substance Painter (probably **2048x2048**)
- Set the **Edge Color** to black
- Hit **Apply and Close** and the file will be saved

<br>

![UV Snapshot](https://user-images.githubusercontent.com/36719180/93838078-7e49ec80-fcdc-11ea-84b7-d5140480fdae.png)

<br>

- Locate that file and open it in **Photoshop**
- Hit **CTRL + A** to *select all*, copy it and paste it in the **Landmine_BaseColor** document - it'll synch up perfectly

<br>

![UV map imported](https://user-images.githubusercontent.com/36719180/93838189-e698ce00-fcdc-11ea-8ed3-2629106cac8a.png)

<br>

Now you can make those adjustments. This may be tricky in regard to certain UV shells, depending how they were unwrapped.. our options are a bit limited, for example, where it comes to the top-down projections of the circular dome.

But we can work with the top-most regions of that dome section, generally adjust colour tones, and readily add detail to the yellow band.

<br>

![Additions made](https://user-images.githubusercontent.com/36719180/93839335-c1a65a00-fce0-11ea-8e1a-c0938bb594e2.png)

<br>

- When you're done, make the UV guide invisible in the **Layers** panel
- Choose **File » Export » Save for Web (Legacy)**
- Either replace the existing file (suggest backing it up first) or save a new version
- Go back into your UE4 project and locate the **Landmine_BaseColor** asset in its folder in the **Content Browser**
- **Right-click** it and either choose **Reimport** (if you replaced the existing file) or **Reimport with New File** if you made a new version
> The BaseColor texture will be updated in all assets that use it

<br>

![Final hero shot](https://user-images.githubusercontent.com/36719180/93839439-0b8f4000-fce1-11ea-8488-bc7c2ccdc958.png)

<br><br>

---

## 004.006 | In summary

<br>

That's it! 

Those are the complete basics of the *Maya » Substance » UE4 3D asset pipeline*.

Next time, we'll cover some intermediate and advanced tips and tricks — importantly, covering collision - but in truth you now have most of the relevant skills used most commonly within the industry.

Enjoy!

<br><br>

---





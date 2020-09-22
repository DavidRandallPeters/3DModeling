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

![Export settings](https://user-images.githubusercontent.com/36719180/93734536-b9411700-fc2d-11ea-808e-70088bbda8a1.png)

<br>

Substance will run the export. You'll notice that the file-names have inherited the name of your Maya shader - most likely this is *lambert1*.

<br>

![Lambert](https://user-images.githubusercontent.com/36719180/93734710-80557200-fc2e-11ea-818c-2e3fcdc822f1.png)

<br>

By all means leave this as is - I'm kinda fussy though - so I'll open the destination folder and tidy up those file names.

<br><br>

---

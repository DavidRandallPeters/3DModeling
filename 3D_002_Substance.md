# 3D Modeling for Game | 002 | Substance


![Banner](https://user-images.githubusercontent.com/36719180/90928812-ad560f80-e44b-11ea-8bc2-cf44378c8e36.png)


Notes prepared by David Peters

Using Maya 2020

---

## 002.001 | Normal maps

<br>

![Ceres normal map](https://user-images.githubusercontent.com/36719180/93048659-8211b980-f6b3-11ea-8281-03e376bb5a10.png)

When preparing 3D assets for use in game engines, we need to save on resources wherever possible. This means trying to lighten the processing load by keeping assets light-weight. You'll have heard the terms *low-poly* and *high-poly* before, now doubt.

In case you're unfamiliar with these terms, we're talking about the polygon count of a 3D mesh. A model's polys can number into the tens of thousands, depending on how it was created and to what detail. Typically, soft-surface models (eg. organic creatures) created in sculpting software (such as ZBrush) will reach these lofty heights - hard-surface models absolutely can too.

It would be a shame if the detail that we achieve when modeling or sculpting was wasted in the process of preparing our assets for use in a game. Fortunately, it doesn't have to be..

Substance has the capability of *'baking'* the detail of a high-poly mesh down to a low-poly mesh. This means that grooves and rivets and creases and wrinkles can be included in what's called a *normal map* - (derived from the high-poly model) - which is projected onto a light-weight low-poly model.

A normal map weighs only as much as a 2D texture, but when read by 3D software and indeed game engines, can massively improve the fidelity of a low-poly model.

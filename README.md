# Additional Products
**Introduction**

Additional Products is a modding framework that allows anyone to add new, fully functional products to Megastore Simulator — no coding required. Drop in a folder with a manifest and a texture, and your product will appear in the game's ordering system, show up on shelves, get delivered by truck, and be purchased by customers just like any vanilla product.

This mod is in **early access** — core functionality is stable and working, with more features on the way.

---

## Features

- Add many new custom products to the game
- Products integrate fully with the ordering products system, delivery trucks, shelves, stock management, and customer purchasing system
- Supports custom icons and textures
- Supports product packs — bundle multiple products in a single folder (Each product must have their own folder still! This is just for organising)
- Auto-assigns product IDs to avoid conflicts between mods
- Products removed from the products folder are automatically cleaned up

---

## Installation

1. Make sure you have already installed Tobey's Bepinex Pack from nexus
2. Download the latest version of Additional Products from Nexus
3. Drop `additionalProducts.dll` into `BepInEx/plugins/`
4. Launch the game once to generate the `BepInEx/plugins/AdditionalProducts/Products/` folder
5. Add your product packs to the `Products/` folder and you're good to go

---
## This mod does nothing by itself, and it does not come with preinstalled products. Other creators have my full permission to release their product packs on nexus for Additional products! Just reference Additional products as a dependency and tell people where to drop your product mod. `BepInEx/plugins/AdditionalProducts/Products/`

## For Mod Authors — Creating a Product

Each product lives in its own folder inside `BepInEx/plugins/AdditionalProducts/Products/`. The folder name doesn't matter, but it should be unique.

There are example products available to view in [here](https://github.com/ApolloVulpez/additionalProducts/tree/main/Example%20Product)

### Folder Structure

```
Products/
  my_product/
    manifest.xml
    textures/
      icon.png
      texture.png
```

You can also group products into packs:

```
Products/
  MyCerealPack/
    ChokiPik/
      manifest.xml
      textures/
        icon.png
        texture.png
    CornFlakes/
      manifest.xml
      textures/
        icon.png
        texture.png
```

Additional Products will scan all subfolders recursively, so any `manifest.xml` it finds will be loaded regardless of how deep it is.

---
### Layout Editing

In game, if you press F10 while looking at a custom product (preferably one you've made) a GUI will open allowing you to move each individual product around from first slot to last. You can also rotate them. All keybinds are listed in game
When you save your custom layout, the mod will automatically make a layout.json file in your products mod directory. Make sure you ship this with your mod, othewise your custom layout will not load for others! and do not edit the file!
When adding new slots to the shelf to have more products on the shelf, you may need to add the slots first, save and then add more products before you can edit the layout. And before you delete slots make sure there are no products on the shelf! This will bug the game out and lose you products.

### manifest.xml

The manifest defines everything about your product. Here's a full example:

```xml
<Product>
    <Name>Chokipik</Name>
    <Brand>ChocoFoods</Brand>
    <BaseProduct>CEREAL</BaseProduct>
    <ProductGroup>GROCERY</ProductGroup>
    <ShelfType>SHELF</ShelfType>
    <BoxType>SMALL_BOX</BoxType>
    <Height>0.08366193</Height>
    <Cost>1.20</Cost>
    <UnitMarketPrice>2.49</UnitMarketPrice>
    <ShelfRowCount>5</ShelfRowCount>
    <ShelfColumnCount>4</ShelfColumnCount>
    <BoxRowCount>3</BoxRowCount>
    <BoxColumnCount>6</BoxColumnCount>
    <IsVerticalBoxLayout>false</IsVerticalBoxLayout>
    <RequiredLicense>1</RequiredLicense>
    <FacePlayer>true</FacePlayer>
    <Scale>1,1,1</Scale>
    <LocalPosition>0,0,0</LocalPosition>
</Product>

# Optional:
    <Scale2>1,1,1</Scale2>
```

### Field Reference

| Field | Description | Example |
|---|---|---|
| `Name` | Display name of the product | `Chokipik` |
| `Brand` | Brand shown beneath the name in the shop UI | `ChocoFoods` |
| `BaseProduct` | The existing game product to clone the 3D mesh from | `CEREAL` |
| `ProductGroup` | The department this product belongs to | `GROCERY` |
| `ShelfType` | What type of shelf this product can be placed on | `SHELF` |
| `BoxType` | The box type used for storage and delivery | `SMALL_BOX` |
| `Height` | Some products such as t-shirts require this to stack on top of each other | `0` |
| `Cost` | Wholesale cost per unit | `1.20` |
| `UnitMarketPrice` | Suggested retail price | `2.49` |
| `ShelfRowCount` | How many rows of product fit on a shelf | `5` |
| `ShelfColumnCount` | How many columns of product fit on a shelf | `4` |
| `BoxRowCount` | Rows of product per delivery box | `3` |
| `BoxColumnCount` | Columns of product per delivery box | `6` |
| `IsVerticalBoxLayout` | Some products stack on top of each other in boxes, this allows that. | `false` |
| `RequiredLicense` | License level required to unlock (1 = first license) | `1` |
| `FacePlayer` | Whether the product faces the player when in a box (Some products rotate weird if this is false, so experimentation is required for your product) | `true` |
| `Scale` | Visual scale of the product mesh (x,y,z) | `1,1,1` |
| `LocalPosition` | Allows you to offset the products on the shelves in the XYZ axis. This will fix any clipping issues when aligning products | `0,0,0` |

### Optional Fields

| Field | Description | Example |
|---|---|---|
| `Scale2` | Some products may have multiple parts to them, such as T-Shirts (Folded and on hangers). Scale will handle folded, and scale 2 will handle the hangers | `1,1,1` |

---

### Valid Values

**ProductGroup**

Find all valid Product Groups in [Product Groups.md](https://github.com/ApolloVulpez/additionalProducts/blob/main/Product%20Groups.md)

**ShelfType**

Find all valid Shelf Types in [Shelf Types.md](https://github.com/ApolloVulpez/additionalProducts/blob/main/Shelf%20Types.md)

**BaseProduct**

Any valid product type name from the game. See the full list of available base products and their textures in [Product Types.md](https://github.com/ApolloVulpez/additionalProducts/blob/main/Product%20Types.md). 

If you are struggling to figure out what your product that you are using as a foundation is called, you can use the [Type Names.md](https://github.com/ApolloVulpez/additionalProducts/blob/main/Type%20Names.md) file as it contains all translations from ingame name to product type name. Such as `CD_01 = Alone Handprint CD` CD_01 is the type name. Alone Handprint CD is the ingame name in english. Unfortunately all names are in english so if you play in a different language you may struggle to find your type name, sorry.

A new resource I just added recently is [ProductDatas.yaml](https://raw.githubusercontent.com/ApolloVulpez/additionalProducts/refs/heads/main/ProductDatas.yaml) This contains every product type with its respective data. Just search for your product type, and it will  tell you the default shelf rows, columns, box rows etc!

### Note: T-Shirts use scale 2.08 in the base game, so if you're making a T-Shirt product, make sure to set the scale to `2.08, 2.08, 2.08` otherwise they will be really small. 
---

### Textures

Place your textures in the `textures/` subfolder next to your `manifest.xml`.

| File | Purpose |
|---|---|
| `icon.png` | The product icon shown in the shop UI |
| `texture.png` | The texture applied to the product's 3D mesh |

For `texture.png` — you can take the texture currently in use for the model you are using as a base, and apply your texture over the top, then just drop the editted texture into the texture folder. You're basically replacing the texture from the old model with your texture. Remember positioning matters! Use the old texture as a foundation for your custom one so everything lines up. All textures will be available next to the product type in Product Types.md referenced above.

There is also a template available for CEREAL that shows you how to properly lay your texture out, also comes with a PSD file for Photoshop. This was kindly created by SchneakySchteveTTV over on discord
Find it here: [CEREAL Template](https://github.com/ApolloVulpez/additionalProducts/tree/main/Templates/Cereal)

---





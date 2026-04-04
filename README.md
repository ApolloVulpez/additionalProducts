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
4. Launch the game once to generate the `BepInEx/plugins/AdditionalProducts/products/` folder
5. Add your product packs to the `products/` folder and you're good to go

---
# This mod does nothing by itself, and it does not come with preinstalled products. Other creators have my full permission to release their product packs on nexus for Additional products!

## For Mod Authors — Creating a Product

Each product lives in its own folder inside `BepInEx/plugins/AdditionalProducts/products/`. The folder name doesn't matter, but it should be unique.

### Folder Structure

```
products/
  my_product/
    manifest.xml
    textures/
      icon.png
      texture.png
```

You can also group products into packs:

```
products/
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
    <Cost>1.20</Cost>
    <UnitMarketPrice>2.49</UnitMarketPrice>
    <ShelfRowCount>1</ShelfRowCount>
    <ShelfColumnCount>3</ShelfColumnCount>
    <BoxRowCount>2</BoxRowCount>
    <BoxColumnCount>3</BoxColumnCount>
    <RequiredLicense>0</RequiredLicense>
    <FacePlayer>true</FacePlayer>
    <Scale>1,1,1</Scale>
</Product>
```

### Field Reference

| Field | Description | Example |
|---|---|---|
| `Name` | Display name of the product | `Chokipik` |
| `Brand` | Brand shown beneath the name in the shop UI | `ChocoFoods` |
| `BaseProduct` | The existing game product to clone the 3D mesh from | `CEREAL` |
| `ProductGroup` | The department this product belongs to | `GROCERY` |
| `ShelfType` | What type of shelf this product can be placed on | `SHELF` |
| `BoxType` | The box type used for delivery | `SMALL_BOX` |
| `Cost` | Wholesale cost per unit | `1.20` |
| `UnitMarketPrice` | Suggested retail price | `2.49` |
| `ShelfRowCount` | How many rows of product fit on a shelf | `1` |
| `ShelfColumnCount` | How many columns of product fit on a shelf | `3` |
| `BoxRowCount` | Rows of product per delivery box | `2` |
| `BoxColumnCount` | Columns of product per delivery box | `3` |
| `RequiredLicense` | License level required to unlock (0 = always available) | `0` |
| `FacePlayer` | Whether the product faces the player when on a shelf | `true` |
| `Scale` | Visual scale of the product mesh (x,y,z) | `1,1,1` |

---

### Valid Values

**ProductGroup**
Find all valid Product Groups in [Product Groups.md](https://github.com/ApolloVulpez/additionalProducts/blob/main/Product%20Groups.md)

**ShelfType**
Find all valid Shelf Types in [Shelf Types.md](https://github.com/ApolloVulpez/additionalProducts/blob/main/Shelf%20Types.md)

**BaseProduct**
Any valid product type name from the game. See the full list of available base products and their textures in [Product Types.md](https://github.com/ApolloVulpez/additionalProducts/blob/main/Product%20Types.md).

---

### Textures

Place your textures in the `textures/` subfolder next to your `manifest.xml`.

| File | Purpose |
|---|---|
| `icon.png` | The product icon shown in the shop UI |
| `texture.png` | The texture applied to the product's 3D mesh |

For `texture.png` — you can take the texture currently in use for the model you are using as a base, and apply your texture over the top, then just drop the editted texture into the texture folder. You're basically replacing the texture from the old model with your texture. Remember positioning matters! Use the old texture as a foundation for your custom one so everything lines up. All textures will be available next to the product type in Product Types.md referenced above.

---

## Planned Features

- **Custom OBJ mesh support** — bring your own 3D model instead of cloning an existing product's mesh
- More manifest fields for fine-grained control over product placement and behaviour




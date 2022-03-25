![Workshop_header_template](/Workshop_header_template.png)
# Blender Portrait scene

## Table Of Contents

   * [Introduction](#introduction)
   * [Provided Files](#provided-files)
   * [Instructions to create a portrait](#instructions-to-create-a-portrait)
      * [Step 1) Open the blender scene &amp; Import your assets.](#step-1-open-the-blender-scene--import-your-assets)
      * [Step 2) Link pose action](#step-2-link-pose-action)
      * [Step 3) Pose &amp; Render](#step-3-pose--render)
      * [Step 4) Update in-game portrait](#step-4-update-in-game-portrait)
         * [Portrait Types](#portrait-types)
   * [Blender Scene Breakdown](#blender-scene-breakdown)
      * [Tabs](#tabs)
         * [Main](#main)
         * [Shading](#shading)
            * [World shader setup](#world-shader-setup)
            * [Horse colour](#horse-colour)
         * [Rendering](#rendering)
      * [Collections](#collections)
         * [Cameras](#cameras)
         * [Lights](#lights)
         * [Floor](#floor)
            * [Grass](#grass)
            * [Sea](#sea)
         * [Pose_Reference_Text](#pose_reference_text)
         * [Proxy_Character](#proxy_character)
         * [Extra_Objects](#extra_objects)
            * [Boat extras](#boat-extras)
         * [Imported_Character](#imported_character)
   * [TWRR: Units card info - Modders spreadsheet](#twrr-units-card-info---modders-spreadsheet)
      * [Portrait_info](#portrait_info)
      * [Pose_info](#pose_info)

## Introduction

This document reviews the Blender file provided to the modding community for the use of creating render portraits for Total War: Rome Remastered. These are used to create both the unit cards and for the larger unit info images.

|Unit Card|Unit Info|
|------|-----------|
|![Unit Card](/documentation/feature_guides/unitcards/roman_archer_auxillia.png)|![Unit Card](/documentation/feature_guides/unitcards/roman_archer_auxillia_info.png)  |

**NOTE: This is _not_ a tutorial, simply just instructions and tips to render out an image used for portraits.**

## Provided Files

You can find the blender project root folder [here](/documentation/feature_guides/unitcards/TWRR_portrait_render_blender/):

 * TWRR_portrait_render_scene.blend
   * This is a base blender scene that can be used for unit renders
   * This scene was created using version 2.93.0.
 * Supporting files
   * icons
A directory containing the icons which are baked into selected portraits. These can be simply added on top of the portrait after the render. ![unit_icons](/documentation/feature_guides/unitcards/unit_icons.png)

   * textures
     * polyhaven
       * Contains the grass texture used for the floor plane.  This is a free texture from [polyhaven](https://polyhaven.com/) and is set up as a preset example for modders. ![floor_textures](/documentation/feature_guides/unitcards/floor_textures.png)

     * TTWR
       * Contains the TTWR supporting textures, this does not include unit clothing due to the number of textures. You can extract all of the variants from the game data if you are looking to modify a specific unit from the game. ![supporting_textures](/documentation/feature_guides/unitcards/supporting_textures.png)

   * [TWRR: Units card info - Modders spreadsheet](https://docs.google.com/spreadsheets/d/1bj7VtvCx0kVAAXH5HseA8_ZzrFb6ZpXOoJukkjqFxm8/edit?usp=sharing)
     * A spreadsheet containing information about each portrait used in the game.

## Instructions to create a portrait

### Step 1) Open the blender scene & Import your assets.

If in the blender scene the textures appear to be missing (as shown in the example below).
Go to `File / External Data / Find Missing Files /` (navigate to the provided textures directory and hit `Find Missing Files`.

![open_blender_1](/documentation/feature_guides/unitcards/open_blender_1.png)

![open_blender_2](/documentation/feature_guides/unitcards/open_blender_2.png)

Import the unit file. If you are using a unit from TWRR you may notice the unit is very small and the scale needs fixing. Firstly scale the skeleton, which should be automatically selected after the import.

**IMPORTANT** The scale is **0.010** this should be **1.000** Be sure the scale XYZ

![fix_scale](/documentation/feature_guides/unitcards/fix_scale.png)

Secondly, you will notice the geometry is now too big, this is due to unit conversion (inches and meters). **The scale is 1.000 this should be 0.3937**

**NOTE:** Be sure the scale XYZ - This is only for the skinned mesh, does not include held props

![fix_scale2](/documentation/feature_guides/unitcards/fix_scale2.png)

This should fix the unit scale. Then set up your materials using the appropriate textures (skipped skin textures for this example).

![fix_textures](/documentation/feature_guides/unitcards/fix_textures.png)

### Step 2) Link pose action

This will work if the skeleton is set up the same way as the TWRR unit skeleton (this includes slingers).

_ie: the Armature bone names & the Skinned Geometry vertex groups are consistently named.
If a vertex name does not match a bone name, the skinning will not work._

![link_pose_action1](/documentation/feature_guides/unitcards/link_pose_action1.png)

![link_pose_action2](/documentation/feature_guides/unitcards/link_pose_action2.png)

1. Select the imported character's skeleton.
2. Navigate to the Action Editor / Browse Action to be linked (icon)
3. Select Action:unit_poses

The imported skeleton will now pose the same way as the proxy unit.

### Step 3) Pose & Render

![pose_n_render1](/documentation/feature_guides/unitcards/pose_n_render1.png)

![pose_n_render2](/documentation/feature_guides/unitcards/pose_n_render2.png)

Each pose is on a keyframe on the timeline, scrub through the timeline until you find a pose you like and render (F11). Don't worry about the proxy character, the collection is not set to render.
You can also edit the pose if you wish or add your own. (Just remember to keyframe the bones you pose)

![pose_n_render3](/documentation/feature_guides/unitcards/pose_n_render3.png)

The render will appear, then save it as a TGA (as that is the expected format in the game). Make sure the image is named the same as the portrait you want to update.
(For this example we will update the roman Julii archer main portrait only `#roman_archer.tga` **NOT** including the info version)

**NOTE: The resolution by default is set pretty high, we suggest you lower it for in-game (164x224)**


### Step 4) Update in-game portrait

Simply update the file in-game and that should work.
Navigate to the game data files and you can find the portrait directories here:

**Portrait game directories**
  * Game Directories
    * **BASE** - `...\Contents\Resources\Data\data\ui`
    * **BI** - `...\Contents\Resources\Data\bi\data\ui`
    * **ALEX** - `...\Contents\Resources\Data\alexander\data\ui`
  * Subdirectories:
    * `...\unit_info`
    * `...\unit_info_classic`
    * `...\units`
    * `...\units_classic`

#### Portrait Types

There are a total of 4 types of portraits you can update, 2 for Modern colours and 2 for Classic colours. The visible portrait will change depending on this setting Settings / Graphics Settings / Unit Colour Scheme.

![portrait_types](/documentation/feature_guides/unitcards/portrait_types.png)

These settings change which directories are referenced to load in the images.

| |Vibrant (original)|Realistic|
|------|------|-----------|
|Directories|unit_info_classic
units_classic|unit_info
units|

Difference between **unit_info** & **units**:

| |unit_info|units|
|------|------|-----------|
| Differences | Is the full render portrait used in the info tab. ![Unit Card](/documentation/feature_guides/unitcards/roman_archer_auxillia.png) The naming convention is as follows: `portraitname_info.tga` i.e. `assassin_info.tga`, `screeching_women_german_info.tga`) | Is the main portrait. ![Unit Card](/documentation/feature_guides/unitcards/roman_archer_auxillia_info.png) The naming convention is as follows: `#portraitname.tga` (examples: `#roman_generals_guard_cavalry.tga`, `#greek_hoplite_spartan.tga`) `portraitname.tga `(exclusive for: `assassin.tga`, `diplomat.tga`, `merchant.tga`, `spy.tga`)


As you can see, the main portrait has been updated and as the info portrait has not been updated it is still using the roman archer info.
Note: The icons located in the blue outline are not part of the portrait system and are placed on top in-game.

![portrait_types2](/documentation/feature_guides/unitcards/portrait_types2.png)

## Blender Scene Breakdown

### Tabs

There are default tabs in the blender file accordingly, feel free to customize/add your own.

#### Main

General scene setup.

![tabs](/documentation/feature_guides/unitcards/tabs.png)

#### Shading

2 Shading editors are open in this (bottom/middle).
 * Left - Object
 * Right - World
 
 ![shading](/documentation/feature_guides/unitcards/shading.png)

##### World shader setup

 ![worldshadersetup](/documentation/feature_guides/unitcards/worldshadersetup.png)
 
The world shader is using an image file as an HDRI. it is set up to use the **studio.exr** which comes with Blender and can be changed if desired.
 
**NOTE**: If the render comes out "pink like", double-check the path to this image is valid.

##### Horse colour

 ![horse](/documentation/feature_guides/unitcards/horse.png)

The node set up in the shader editor for horses also includes a quick colour override.
If the uvs are **+1 Y** the colour will be mixed.

#### Rendering

Portrait render preview here, you can change the camera by selecting the camera node you want in the outliner (Top right).

 ![render1](/documentation/feature_guides/unitcards/render1.png)
** NOTE:** The camera node is the child of the transform with the green icon
 
 ![render2](/documentation/feature_guides/unitcards/render2.png)

### Collections

 ![collections](/documentation/feature_guides/unitcards/collections.png)
 
 This section is broken down based on the collections used in the file.

#### Cameras

 ![cameras](/documentation/feature_guides/unitcards/cameras.jpg)

#### Lights

 ![lights](/documentation/feature_guides/unitcards/lights.jpg)
 
 ...Action? 

#### Floor

 ![floor](/documentation/feature_guides/unitcards/floor.jpg)

##### Grass

The grass texture provided is free from [polyhaven](https://polyhaven.com/) and is set up as a preset example for modders. The exact texture can be found [here](https://polyhaven.com/a/forrest_ground_01).

 ![grass1](/documentation/feature_guides/unitcards/grass1.png)
 ![grass2](/documentation/feature_guides/unitcards/grass2.png)

##### Sea

Is procedural material using the shader editor and will animate over frames (giving variation for each portrait)

 ![sea1](/documentation/feature_guides/unitcards/sea1.png)
 ![sea2](/documentation/feature_guides/unitcards/sea2.png)

#### Pose_Reference_Text

Simply a reminder of pose id groups.

 ![Pose_Reference_Text](/documentation/feature_guides/unitcards/Pose_Reference_Text.png)

#### Proxy_Character

 ![Proxy_Character](/documentation/feature_guides/unitcards/Proxy_Character.jpg)

#### Extra_Objects

 ![Extra_Objects](/documentation/feature_guides/unitcards/Extra_Objects.jpg)
 
**NOTE:** If the object is a skeleton mesh, the geometry is under the armature node

##### Boat extras

In the sub-collection boat_extras you will find various extras which can be used.
The model Mesh:boat_faction_icon is a plane that contains shape keys to fit onto a specific boat sail (the shape keys are fit to the pose and model listed on the [TWRR: Units card info - Modders spreadsheet](https://docs.google.com/spreadsheets/d/1bj7VtvCx0kVAAXH5HseA8_ZzrFb6ZpXOoJukkjqFxm8/edit?usp=sharing)).
You can use the files in `faction_icons` folder to use on this plane.

 ![boat](/documentation/feature_guides/unitcards/boat.png)

#### Imported_Character

This is an empty group that is active by default. Simply a place to import your characters to.

## TWRR: Units card info - Modders spreadsheet

This sheet contains information for each unit portrait which can be useful for finding out which portrait uses which unit, pose, colours and where the final file should go. Here is a breakdown of each tab.

### Portrait_info

 ![portrait_info](/documentation/feature_guides/unitcards/portrait_info.jpg)

### Pose_info

 ![pose_info](/documentation/feature_guides/unitcards/pose_info.jpg)

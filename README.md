# 2DPsdImporter-6.0.7

Animation with Sprite Resolver 
The psb file is imported with the folder, so that even if layers are added later and the guid changes, it can be updated without breaking the connection between Bone and Sprite no.
![2DPsdImporter-6 0 7](https://user-images.githubusercontent.com/33142993/234664652-604ffc3c-f7a8-4afb-bb70-285ad3a21768.gif)

After importing psb, you can no longer set Category and Label of layers in SkinnEditor from Unity2021
   Create a new Sprite Library Asset, Skeleton Asset and save it to a psb file
   psbfile (project inspector) -> Character Rig: Main Skeleton
   psbfile (hierarchy inspector) -> Sprite Library: Main Sprite Library Asset
   set to

   If you have set Category Label or Skeleton (bone) before Unity2021, in Unity Project -> psb file
   Since Sprite Library Asset and Skeleton Asset are stored (because it has become a ReadOnlyFile), copy and use it

   * In the settings of the PSD Importer on the psbfile inspector
   LayerImport -> LayerMapping: Use Layer Name
   If you do, the state of the Character will not be destroyed even if you add a layer to the psbfile later and overwrite it.
   If you don't do this, you'll need to redefine the connection between Sprite and Bone on the SkinnEditor.

   * Sprite Editor -> Skinning Editor settings for Bone and Sprite strings
   Assets/Resources/Characters/Akane2D/Akane2D2.psb.meta is edited and reflected
   So if you want to make the Bone and Sprite of the psb file created before Unity2020 fully compatible with the new SkinnigEditor after Unity2021
   (If you want to separate Sprite Library Asset, Skelton Asset from psb file) Sprite Editor -> Skinning Editor only settings with Bone and Sprite strings
   need to do it again

   Bone and Sprite Stringed Settings
   Select psbfile -> Open Sprite Editor
   Open the Skinnig Editor, press Visibility on the top right of the screen, select the Sprite tab in the Bone and Sprite tabs
   Assign Bone from Geometry -> Bone Influence to each Sprite
   After assigning bones to all sprites, set the range of bones that affect the sprites from Geometry -> AutoGeometry
   When everything is finished, press the Apply button on the upper right of the Window


   How to generate Skeleton assets
   → In short, when you import a psb file and set Bone in the Skinning Editor, it is automatically generated inside the psb file (ReadOnly)
   If you want to go outside, copy it and set it to Main Skeleton
   https://docs.unity3d.com/Packages/com.unity.2d.psdimporter@5.0/manual/PSD-importer-properties.html#main-skeleton
   main skeleton
   A skeleton asset (.skeleton) is an asset containing a bone hierarchy that can be animated in any 2D animation package.
   The Main Skeleton property is only available if you've imported a .psb file with the Character Rig importer setting enabled.
   After importing the .psb file, assign the .skeleton asset to the Main Skeleton property so that the generated prefab character will be automatically rigged with the bone hierarchy contained in that .skeleton asset.


   If there is no .skeleton asset assigned to the Importer's Main Skeleton property, a .skeleton asset is automatically generated as a sub-asset of the imported source file and named '[Asset File Name] Skeleton'.
   You can share a .skeleton asset between different generated prefabs by assigning the same .skeleton as the main skeleton property on import.

   * Can't edit bones of exported Skeleton Asset in Skinnig Editor
   https://docs.unity3d.com/Packages/com.unity.2d.psdimporter@8.0/manual/skeleton-sharing.html
   Bone Tools in the Skinning Editor are disabled when an actor references another actor's .skeleton asset instead of its own.
   To edit the bones, open the original actor (which the .skeleton asset belongs to) in the Skinning Editor and edit the bones.
   Changes to the original .skeleton asset will be reflected in all Actors that reference it.
   In this example, changes made to the "primary skeleton" are reflected in the bone hierarchy of the "variant" actor.

   So basically Skeleton Asset should be considered as a pair with psb file, it seems better not to go out
   If nothing is specified for Character Rig->Main Skeleton in the psb file's inspector, it will reference her Skeleton Asset in her own psb file

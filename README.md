# Fallout 4 VR setup

This is a guide to set up Fallout 4 VR.

# Table of Contents
- [Fallout 4 VR setup](#fallout-4-vr-setup)
- [Table of Contents](#table-of-contents)
- [0. Modding tools](#0-modding-tools)
  - [0.1 INI file configuration](#01-ini-file-configuration)
  - [0.2 Vortex](#02-vortex)
  - [0.3 Fallout 4 VR Script Extender](#03-fallout-4-vr-script-extender)
- [1. Teleport](#1-teleport)
  - [1.1 Increase distance](#11-increase-distance)
  - [1.2 Decrease stamina consumption](#12-decrease-stamina-consumption)
  - [1.3 Decrease duration](#13-decrease-duration)
  - [1.4 Decrease teleport marker size](#14-decrease-teleport-marker-size)
- [2. Disable camera pushback](#2-disable-camera-pushback)
  - [2.1 Remove object collision](#21-remove-object-collision)
  - [2.2 Remove NPC collision](#22-remove-npc-collision)
- [3. World size](#3-world-size)
  - [3.1 Player size](#31-player-size)
  - [3.2 Skybox size](#32-skybox-size)
- [4. Rendering](#4-rendering)
  - [4.1 Increase sharpness](#41-increase-sharpness)
  - [4.2 Increase FPS](#42-increase-fps)
- [5. Optional improvements](#5-optional-improvements)
  - [5.1 Disable intro](#51-disable-intro)
  - [5.2 HUD Tweaks](#52-hud-tweaks)
    - [Disable enemy health bars](#disable-enemy-health-bars)
    - [Disable compass](#disable-compass)
    - [Lower compass](#lower-compass)
    - [Only show HP/ammo when pointing gun up](#only-show-hpammo-when-pointing-gun-up)
    - [Smaller HP/ammo HUD](#smaller-hpammo-hud)
  - [5.3 Interaction distance](#53-interaction-distance)
    - [Follower activation](#follower-activation)
    - [Item pickup](#item-pickup)
    - [Item activation](#item-activation)
  - [5.4 Grenade controls](#54-grenade-controls)
- [6. DLC](#6-dlc)
- [7. Mods](#7-mods)
  - [7.1 Performance](#71-performance)
  - [7.2 Fixes](#72-fixes)
    - [Unofficial patch](#unofficial-patch)
    - [Index/Cosmos controller support](#indexcosmos-controller-support)
    - [Binaural 3D Surround Sound](#binaural-3d-surround-sound)
  - [7.3 Additions](#73-additions)
    - [Hand models `(F4VRSE required)`](#hand-models-f4vrse-required)
    - [Quick slots `(F4VRSE required)`](#quick-slots-f4vrse-required)
    - [Inventory management `(DLCs required)`](#inventory-management-dlcs-required)
    - [Immersive power armour helmets](#immersive-power-armour-helmets)
    - [Show full dialog](#show-full-dialog)

# 0. Modding tools

## 0.1 INI file configuration

Fallout 4 VR can be configured via the INI file `%USERPROFILE%\Documents\My Games\Fallout4VR\Fallout4Custom.ini`.
This file will be automatically created when you first launch Fallout 4 VR.
This guide will contain multiple examples of INI settings, which all show a category and settings below it, e.g.

```ini
[category]
setting=value
```

INI file settings can be listed and changed runtime by opening the console with `~` and using the following commands:

 - `SetINI "setting:category" value` is used to change a setting e.g. `SetINI fVrScale:VR 73` 
 - `GetINI "setting:category"` can be used to get the current value of a setting
 - `saveini` is used to save changed settings to the ini files
 - `refini` is used to load changes made to the ini files 

## 0.2 Vortex

Not everything in Fallout 4 VR can be fixed via the INI file. 
Luckily, the game has a large modding community. 
The easiest way to install mods is via [Vortex](https://www.nexusmods.com/about/vortex/); a modding tool that supports direct downloading of games via www.nexusmods.com, fixes mod loading order, detects redundant mods and more!

It is highly recommended to use the [Version Check Patcher Mod](https://www.nexusmods.com/fallout4/mods/42497) when modding Fallout 4 VR.
This mods automatically updates all installed mods when an update to Fallout 4 VR is released, making sure you do not have to do this manually.

Note: the following INI configuration might be necessary to enable mods.

## 0.3 Fallout 4 VR Script Extender

[F4VRSE](https://f4se.silverlock.org/) enables a wider ranges of mods than the game engine does by default. 
This guide will indicate which mods require it to run.

**Note that using this requires the game to be launched via a different executable, breaking the launch button in Steam.**

```ini
[Archive]
bInvalidateOlderFiles=1
sResourceDataDirsFinal=
```

# 1. Teleport

The default teleport functionality is a short distance dash.
To make it feel more like an actual teleport you can use the following tweaks, which all go in `Fallout4Custom.ini` 

## 1.1 Increase distance
```ini
[VRTeleport]
fTeleportDistanceMultiplier=2
```

_Warning! long distance teleporting may prevent you from hitting script trigger zones;
Use this sparingly in scripted events, especially in the tutorial._

## 1.2 Decrease stamina consumption
```ini
[VRTeleport]
fOverEncumberedDrainPerTeleportDistance=0.1
fRunDistanceFactorToEnableSprint=1.800
fSneakDistanceFactorToEnableSprint=1.800
```

## 1.3 Decrease duration
```ini
[VR]
bLerpTeleportEnabled=1
fLerpTeleportDuration=0.00100
```

## 1.4 Decrease teleport marker size
```ini
[VR]
fTeleportTrajectoryScale=0.5
```

# 2. Disable camera pushback

The game pushes you away when you come too close to walls, objects and characters.
This can be disabled to reduce motion sickness.

## 2.1 Remove object collision
```ini
[VR]
fVrHMDMovementThreshold=100
```

## 2.2 Remove NPC collision
Unfortunately, this cannot be done easily via an INI tweak. 
I recommend using the [Player Collision Options](https://www.nexusmods.com/fallout4/mods/41866) mod for this. 

**!! DELETE `[Install directory]/Fallout 4 VR/Data/nocollide_actors_clutter.ini` AFTER INSTALLING THIS MOD !!**

# 3. World size

Finally being able to see everything with depth in Fallout 4 might make you notice some things are a bit off. 

## 3.1 Player size
The player character does not always match the player's actual size. If you feel like you are too small, you can change the following entry;
Find the value between 70 and 80 that matches your height. 

```ini
[VR]
fVrScale=73
```

## 3.2 Skybox size
The default skybox is too close to the player. 
This can be solved with the following entry:

```ini
[VR]
fSkyScaleFactor=5000.0000
```

# 4. Rendering 

The default display settings leave some room for improvement. 
Even with a good GPU you still get blurry images and a low framerate.
Use the following steps to improve performance.

## 4.1 Increase sharpness
The default display settings create a really blurry image.
This can be solved somewhat with the following settings:

```ini
[General]
sStartingConsoleCommand=cl off;taa on;fxaa off
[Display]
iLocation X=555
iLocation Y=90
fTAAPostSharpen=0.675
fTAASharpen=1.0000
fTAAHighFreq=0.8000
fTAALowFreq=0.5000
fTAAPostOverlay=0.675
[VRDisplay]
fRenderTargetSizeMultiplier= 1.0
```

The first line disabled character lighting and FXAA and enables TAA.

The last line changes the supersampling to the default resolution;
It is recommended to instead use your HMD's software to configure supersampling resolution.

If you want to further increase the sharpness the [Contrast Adaptive Sharpening mod](https://www.nexusmods.com/fallout4/mods/48934?tab=description) can be installed. 
**Note that it requires having the ini settings on default, thus omitting the `[Display]` section**.

## 4.2 Increase FPS
By reducing some settings below minimums the FPS can be improved greatly:

```ini
[Display]
iShadowMapResolution=512
```

Furthermore, if you're using Windows 10, check `Fallout4VR.exe>Properties>Compatibility>Disable fullscreen optimizations` and `Fallout4VR.exe>Properties>Compatibility>Change high DPI settings>Override high DPI scaling behavior`.

NVidia users can further improve performance by setting `NVidia Control Panel>3D Settings>Manage 3D Settings>Program Settings>Fallout4VR.exe>Threaded Optimization` to `On`.

# 5. Optional improvements

## 5.1 Disable intro 
```ini
[VR]
bVrShowIntroBink=0
``` 

## 5.2 HUD Tweaks

### Disable enemy health bars
```ini
[VRUI]
bEnemyHealthDynamicScale=0
fEnemyHealthScale=0.0000
```

### Disable compass
The compass can be disabled for extra immersion. The V.A.N.S. skill can show you the path to your next objective and the marker and your direction can be seen on the map in the Pip-Boy.  

```ini
[VRUI]
fHMDHUDStatusScale=0.0000
```

### Lower compass
The compass can also be lowered instead of disabling it. This way it will only be seen when looking down.

```ini
[VRUI]
fHMDHUDStatusZ=-23.0000
```

### Only show HP/ammo when pointing gun up
```ini
[VRUI]
fPrimaryWandHUDPitch=150.0000
```

### Smaller HP/ammo HUD
```ini
[VRUI]
fPrimaryWandHUDScale=0.6000
```

## 5.3 Interaction distance

### Follower activation

Tired of accidentally activating your companion? Use this tweak to only activate when touching them.

```ini
[VR Wand]
fPickDistanceMultiplierForCompanion=0.0000
```

### Item pickup
```ini
[VR Wand]
fPrimaryWandMaxGrabDistance=0.0
fSecondaryWandMaxGrabDistance=0.0
```

### Item activation
```ini
[Interface]
fActivatePickLength=10.0000
fActivatePickRadius=10.0000
```

## 5.4 Grenade controls
Tired of accidentally triggering a grenade instead of reloading? Use this command to increase the button press time for grenade equipment.

```ini
[Controls]
fThrowDelay=1.0
```

# 6. DLC

While Fallout 4 has multiple DLCs available, these are not included in Fallout 4 VR.
They can be copied from Fallout 4 if you own them.
Simply copy `[install directory]/Fallout 4/Data/DLC*.*` to `[install directory]/Fallout 4 VR/Data/`.

We also have to tell the game to load these mods. 
When using Vortex they can simply be enabled through the Plugins tab.
This will add the following lines to `%USER%/AppData/Local/Fallout4VR/plugins.txt`:

```
*DLCRobot.esm
*DLCworkshop01.esm
*DLCCoast.esm
*DLCworkshop02.esm
*DLCworkshop03.esm
*DLCNukaWorld.esm
```

The following fixes are needed to make them work properly, since these DLCs were not created for VR:

- [DLCVR - Fallout 4 VR and DLC standalone bug fixes
](https://www.nexusmods.com/fallout4/mods/28842)
- [Automatron DLC VR FIX](https://www.nexusmods.com/fallout4/mods/34741)
  - **NOTE**: It is recommended to read the [Robot workbench VR README](https://www.nexusmods.com/fallout4/mods/34741?tab=docs); the fixed VR version behaves differently from the regular one:
    - Robot workbench can only be built after completing the General Atomics quests, even though you get the blueprints earlier.  
    - Robot workbench needs to be powered. Build it on a concrete slab and remove the slab to create the space for the wire.
    - Robot workbench does not require robot parts to build robots.
    - Robot workbench can only modify a robot with an empty whiskey bottle in its inventory. (new robots spawn with one in the inventory). **Make sure there is only one robot with a bottle.**
    - **Do not use an existing robot to attach the Jezebel head.** Create a new robot using the `[RESET]` and `[Must Select this to initiate build process]` options, and select the `[Select for DLC01 Quest Objectives]` option to add the Jezebel head before exiting the menu. Otherwise you will not be able to talk to Jezebel.
- [Cait Perk Fix for Automatron DLCVR](https://www.nexusmods.com/fallout4/mods/40794)

# 7. Mods

## 7.1 Performance
To improve the performance even further we can use the following mods:

- [Insignificant Object Remover](https://www.nexusmods.com/fallout4/mods/9835)
- [Fog Remover](https://www.nexusmods.com/fallout4/mods/31976) (Highly recommended, requires DLC)
- [Lucid Institure](https://www.nexusmods.com/fallout4/mods/46580) (Highly recommended)
- A texture pack of choice:
  - [Optimized Vanilla Textures](https://www.nexusmods.com/fallout4/mods/1204)
  - [Texture Optimization Project](https://www.nexusmods.com/fallout4/mods/978)
  - [Complex Retexture Project](https://www.nexusmods.com/fallout4/mods/23352)
  - [Vivid Fallout](https://www.nexusmods.com/fallout4/mods/25714) (Choose 'Best Performance')

## 7.2 Fixes

### Unofficial patch
Vanilla Fallout 4 is quite buggy; luckily an unofficial patch was made by modders.
Download the following mods to make the game more stable:

- [Unofficial Fallout 4 Patch](https://www.nexusmods.com/fallout4/mods/4598)
- [Unofficial Fallout 4 VR Fix](https://www.nexusmods.com/fallout4/mods/47117)

### Index/Cosmos controller support
Simulating vive controllers with the index touchpads makes for a very frustrating control scheme. To fix this you can use the [Oculus touch emulation mod](https://www.nexusmods.com/fallout4/mods/41931). If you have also installed the Contrast Adaptive Sharpening mod you should enable the controller support by setting `enable_oculus_emulation_fix` to `true` in `[install directory]/Fallout 4 VR/fo4_openvr.cfg`. The index controller scheme that is supposed to be used with this is called "*Index as touch w/ custom openvr dll*".

And reduce the rotation sensitivity in workshop mode with the following tweak:

```ini
[Workshop]
fItemHoldDistantSpeed=5.0000
fItemRotationSpeed=1.0000
```

Lastly, you can invert the map scrolling with

```ini
[VRPipboy]
fTouchpadMapPanSpeed=-30
```

### Binaural 3D Surround Sound
This is a [mod](https://www.nexusmods.com/fallout4/mods/39692) that uses Head Related Transfer Functions, which refers to the way that the curvature
of one's ears are used to localize sound in 3D space. 

## 7.3 Additions

Not all mods are used to fix and improve the game. Some add new features as well!
Here are some interesting mods that make playing in VR more fun!

### Hand models `(F4VRSE required)`
[Idle hands](https://www.nexusmods.com/fallout4/mods/42922) replaces the in-game controller models with (static) hands.
It requires multiple other mods and takes some effort to set up,
including manually editing the `plugins.txt`, which clashes with Vortex's automatic generation of this file.

### Quick slots `(F4VRSE required)`
The [VRCustomQuickSlots](https://www.nexusmods.com/fallout4/mods/45170) mod allows you to equip items and consumables from specific slot areas on your body.

[Virtual Holsters](https://www.nexusmods.com/fallout4/mods/51224) does a similar thing, but has fewer problems with naming collissions.

### Inventory management `(DLCs required)`
[Valdacil's Item Sorting mod](https://www.nexusmods.com/fallout4/mods/3877) adds tags to items for more logical sorting.

### Immersive power armour helmets
[Kabuto:VR](https://www.nexusmods.com/fallout4/mods/35909) is an immersive Power Armor helmet replacement mod for 'Fallout 4 VR' which replaces the lackluster semi-transparent Power Armor HUD with a selection of fully enclosed helmets based on the games original helmet meshes

### Show full dialog
Rather than showing some vague hints as to what your character will say, [Full Dialog VR](https://www.nexusmods.com/fallout4/mods/28516) will show you the exact dialog.

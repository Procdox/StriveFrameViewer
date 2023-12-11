# Strive Frame Viewer

This is a fork of Ryn's Advantage viewer mod that allows you to see a SF6 style frame data display in training mode (and only training mode).

## Installation
Download the ue4ss and Frame Viewer zip files from releases, and extract the contents into the win64 directory of GGST. 

e.g. ```C:\Program Files (x86)\Steam\steamapps\common\GUILTY GEAR STRIVE\RED\Binaries\Win64```

## The view explained
Two bars along the bottom of the screen display a series of frames. The top bar corresponds to player one, the bottom bar to player two. The color of these frames indicates different states that the respective player is in.
- <span style="color:gray">Gray</span>: the player is idle 
- <span style="color:blue">Blue</span>: the player is stunned
- <span style="color:yellow">Yellow</span>: the player is in an animation
- <span style="color:red">Red</span>: the player has active hurtboxes
- <span style="color:orange">Red</span>: the player is in a recovery animation

If the training mode reset is triggered (currently hard coded to Right Thumbstick button) or both players don't input a move for 20 frames, the combo is considered "ended" and the display will reset on the next input move.

Additionally, there are some space saving features. If a segment of frames is longer than 5 frames, the total length will be displayed as text. If an animation is in hitstun or counterhit stun, where animation is freezed, the frames will be dropped to save space. If both players have been in the same state for more than 10 frames, the segments will be "truncated" to save space. 



## TODO:
- Fix "off by one" errors where the length of sections is incorrect for some moves, I think this comes down to consequences the odd (but rational in context) way that Strive encodes frame data in bbscript.
- Fix some projectiles and moves not displaying active hitbox frames.
- Fix some cases where idle total time is not displayed.
- Fix total time getting cut off if greater than 100 frames.
- Differentiate between block stun and hitstun
- Add controls to toggle or adjust features like segment truncation

## Disabling
The simplest way to disable this and any other ue4ss mods is to delete or remove the ```dwmapi.dll``` file from the game files. If this file is not present, the rest of the mod will not be loaded when the game is launched.

## Disclaimer
This is not a standard mod that extends or patches Unreal pak data, but instead relies on code injection. While it is designed to only provide functionality in training mode, it may violate TOS with Arc Systems. Using this may result in actions against your account on their part.

I make no guarantees on account standing, game stability, or the mental stability of the user after practicing perfect frame traps that may come as a result of this mod.

I advise disabling this mod (as detailed above) and restarting the game before playing online.

## Compiling from source

1. Download the project, you will need a github account with permissions to download the Unreal repository to do so (see the dependent UE4SS repository for instructions on this)
2. Navigate to ```RE-UE4SS/VS_Solution``` and run ```generate_vs_solution.bat```
3. Open the solution ```Output/UE4SSMods.sln``` in MSVC (I use 2022)
4. Build all
5. There will be several files you need to copy to the game files
    1. ```Output/Output/<build>/UE4SS/bin/UE4SS.dll``` to ```Win64/```
    2. ```Output/Output/<build>/bin/proxy/bin/dwmapi.dll``` to ```Win64/```
    3. ```Output/StriveFrameData/<build>/StriveFrameData.dll``` to ```Win64/Mods/StriveFrameData/dlls/```
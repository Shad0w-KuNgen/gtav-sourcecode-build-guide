![Icon](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/assets/146978592/39674bde-9c2e-4800-99e5-7fc3a05a08f4)
# GTA V Modified Source Code Build Tutorial/Guide

Github edition with fixed links and added some files and features!<br>Based on this [rentry.co](https://www.rentry.co/gtavbuildguide) tutorial, But this tutorial is better than that.<br>

**Working Status:** Working and Tested by me!

## Requirements
### Base
 - Minimum 150GB Free Space
 - GTA V Files from Steam, Epic Games or Social Club (Minimum v2699)
    - Cracked Game is not recommended, in my opinion ther are maybe some problems occur. 
 - GTAVSP.7z<br>
    - **Want to have the source code? [See Here](/misc/gtavsourcecodelinks.txt) for the links and magnet.**<br>
      - You can verify the authenticity of the file by its SHA1 hash: `ca39323730ed644fa534a2946506d4287f92a799`<br>
      - To verify with 7-Zip, right click the file and select `7-Zip > CRC SHA > SHA1`<br>
      - Archive password: `Mi76#b>9mRed`
 - [update.rpf and update2.rpf from GTA V build 2699](https://mega.nz/folder/O1UFlaAB#mqhLDQT7p77sMUnANJDjmA/file/Ph9FlQSK) 

### Dependencies
 - Windows 10/11
    - [LTSC 2021](https://archive.org/download/Windows10EnterpriseLTSC202164Bit/en-us_windows_10_enterprise_ltsc_2021_x64_dvd_d289cf96.iso) Recommended, but you can use Normal Windows 10/11 too.
 - [Visual Studio 2012](https://files.dog/MSDN/Visual%20Studio%202012/en_visual_studio_ultimate_2012_x86_dvd_2262106.iso)
    - [Update 4 for Visual Studio 2012](https://files.dog/MSDN/Visual%20Studio%202012%20Update%204/mu_visual_studio_2012_update_4_x86_dvd_3161759.iso)
 - [DirectX SDK June 2010](https://download.microsoft.com/download/A/E/7/AE743F1F-632B-4809-87A9-AA1BB3458E31/DXSDK_Jun10.exe)
 - [Incredibuild 4.0](https://xoreax-incredibuild.software.informer.com/4.0/)
    - This is only needed for Compiling Shaders and Game Scripts.
 - (OPTIONAL) [3D Studio Max 2010 SDK](https://archive.org/details/sdk-3ds-max-2010)
 - [7-Zip](https://7-zip.org/a/7z2301-x64.exe)
    - For extracting the archives.
 - [OpenIV](https://openiv.com/WebIV/guest.php?get=1)
    - For editing the game files.

### Miscellaneous
 - [Rush Patches](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/files/14641602/rush_patches-master.zip)
 - [DLL Patches](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/files/14641382/dll_patches.zip)
 - (OPTIONAL) [3rdParty Folder](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/files/14733468/3rd.zip)
    - Put this to `X:\gta5\`

## Prebuilt Files
 - [Shaders](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/files/14649717/common.zip)
 - [Scripts](https://drive.google.com/file/d/1AVMC_MBPpqKp0BIrOI-_lLq98QmwRn46/view)

> [!NOTE]
>	It is recommended to create a virtual machine for this build process,<br>although the build process can be done on your Real PC.<br>
>       VMWare/Hyper-V are recommended to run the VM due to their performance.

## Prerequisite Setup
1. Install DirectX SDK June 2010 and 7-Zip
2. Install Visual Studio 2012
   - Uncheck all optional components in the installer **except "Microsoft Foundation Classes for C++"** to save space, none of them are needed for the build.
3. Install Update 4 for Visual Studio 2012
4. Install Incredibuild 4.0 (Only needed for compiling shaders and scripts)
   - If you encounter the error that the installer is "Blocked by your administrator", follow these steps:
   1. Hold Shift and right click the `incredibuild4_0.exe` file, select "Copy as path"
   2. Open Command Prompt as Administrator
   3. Paste the path and press Enter
   - Select to install "Incredibuild Agent", "Incredibuild Coordinator", and the extension for Visual Studio
5. (OPTIONAL) Install 3D Studio Max 2010 SDK
6. Install OpenIV
7. Install Miscellaneous Files
8. Create X:\ drive by following these steps at the bottom
   1. Open Command Prompt
   2. Create a new folder called "GTA" to the Desktop 
   3. Run `net use X: \\localhost\c$\<Path to working folder for build> /persistent:yes`
       - Example: `net use X: \\localhost\c$\Users\abcd\Desktop\GTA /persistent:yes`
9. Create the folder `X:\gta5` and copy all folders from `GTAVSP.7z\GTA V Source` into it
   - By the end, you should have the folders `X:\gta5\src`, `X:\gta5\script`, and `X:\gta5\tools_ng`. If the paths are different or some folders are missing, try re-extracting or moving as needed.
10. Right click the folder `X:\gta5`, select "Properties", uncheck "Read-only", click Apply then OK
11. Copy all folders in `dll_patches.zip` to `X:\gta5\tools_ng\bin`, make sure to overwrite when copying
12. Open Command Prompt as Administrator and run the following commands, then close:
```batch
setx /m RS_TOOLSROOT X:\gta5\tools_ng
setx /m DXSDK_DIR "C:\Program Files (x86)\Microsoft DirectX SDK (June 2010)"
setx /m RS_CODEBRANCH X:\gta5\src\dev_ng
setx /m RS_PROJECT gta5
```
12. To ensure changes are finalized, restart build machine.

## Patching The Source Code
1. Open `rush_patches-master.zip`
2. Copy `game` and `rage` folders to `X:\gta5\src\dev_ng`, make sure to overwrite when copying
3. (OPTIONAL) To skip launcher requirement for running the game, copy `game` and `rage` folders from `OPTIONAL_FIXES` to the same folder

## Building The Game Binary
1. Run `X:\gta5\src\dev_ng\game\VS_Project\load_sln_unity_2012.bat`
	- If prompted with "How do you want to open this file?", check "Always use this app to open .sln files" and click OK.
2. Once the solution loads, open the dropdown menu that says "Debug" at the top, select "Configuration Manager"
3. Change "Active Solution Platform" to "x64" and close the configuration window
4. Hold Ctrl key and click all projects under "GameLibs" and "Rage", right-click and select "Properties"
5. In the "Configuration" dropdown, select "All Configurations"
6. Select `C/C++ > All options`, under "Look for options or switches", search "err" and set "Treat Warnings as Errors" to "No (/WX-)", then click "Apply" and "OK"
   - For faster compiles, search "mul" and set "Multiprocessor Compilation" to "Yes (/MP)".
   - If you get the error `C1060: Compiler is out of heap space` during build, come back to the above setting and turn it off.
7. Right-click the "game" project and select "Properties" and do step 5 again
8. Change build the type at the top of the window from "Debug" to "BankRelease"
9. At the top of the window, select `Build > Build Solution` and wait for build to finish.
10. Copy output binary to game folder.

> [!NOTE]
> Building shaders and scripts can be skipped using the prebuilt files above. These steps are here to allow modding or for those who prefer to build from source as much as possible.

## Building Shaders
1. Under "Shaders", right click the "shaders_rc" project and click "Build"
    - If you building in "BankRelease", Dont forget to build shaders with "Release Win32 4.0" in **Configuration Manager**.
    - Also, the same thing needs to apply to "shaders_dependency", Change "Debug" to "Release" in **Configuration Manager**
    - **If you compiling with Debug, then ignore the steps at the top and continue reading the tutorial.**
2. (OPTIONAL) Build low quality shaders
   1. Right click the "shaders_rc" project and click "Properties"
   2. Select `Configuration Properties > NMake`
   3. Under "General", change all command lines from ending with `win32_40.bat` to ending with `win32_40_lq.bat`, then click "Apply" and "OK"
   4. Rebuild shaders
   3. Copy `X:\gta5\titleupdate\dev_ng\common` to game directory

## Building Game Scripts
1. Open Command Prompt
2. Run the following commands:
```batch
X:
cd X:\gta5\src\dev_ng
setenv
cd ..\..\tools_ng\bin\RageScriptEditor
ragScriptEditor
```
3. In the editor, select `File > Open Project` and open `X:\gta5\script\dev_ng\singleplayer\GTA5_SP.scproj`
4. Select `Compiling > Intellibuild > Build Project`

## Patching Game Assets
1. Run OpenIV, select "Windows"
2. Select the game folder and click "Continue"
3. Open `GTA V\update\update2.rpf\x64\levels\gta5\script`
4. Click the "Edit mode" button, and copy `X:\gta5\titleupdate\dev_ng\x64\levels\gta5\script\script.rpf` to the OpenIV window
5. [IMPORTANT] Fix Story Mode
	1. Open `GTA V\update\update.rpf\common\data` and make sure "Edit Mode" is enabled
	2. Under "XML Text Files", right-click `gameconfig.xml` and click "Edit"
	3. Under "Search", type "51000"
	4. Change the value of `51000` to `53000`
	5. Click "Save"
6. Close OpenIV
7. From `rush_patches-master.zip`, copy all files in the `ARCHIVEFIX` folder to a separate location
8. Open `<GAME FOLDER>\update`, and drag `update.rpf` and `update2.rpf` onto `ArchiveFix.exe`
9. Close both windows

## Running The Game
1. In the game directory, create a file named `launch.bat` and add these contents:
```batch
cd %~dp0
game_win64_bankrelease.exe -noSocialClub -nokeyboardhook -nonetlogs
```
2. (OPTIONAL) Add additional arguments:
 - `-kbgame` - Start game with game keyboard enabled.
 - `-output` - Show console log of game.
 - `-rag` - Enable support for RAG, the internal game debugging tool.
 - `-ragUseOwnWindow` - Use it with `-rag` parameter to make game run outside of RAG Render Window.
 - `-DoReleaseStartup` - Start real Story Mode on launch, Ignore if it says unknown parameter/command.
    - If you dont type this parameter, you will spawned in a random location as a random character with a random clothes. 
 - `-sc_DisableForbiddenVehicleRemoval` - This parameter allows DLC and Other Cars without getting removed.
    - If you using RAG, go to "Vehicles" tab and create widgets, after that Click "Creation Options" and turn on "Create as personal vehicle" to prevent game crashes. 
 - Additional standard game arguments can be added as well.
3. (OPTIONAL) Launch RAG with the following commands in Command Prompt
```batch
X:
cd X:\gta5\src\dev_ng
setenv
cd ..\..\tools_ng\bin\rag
rag
```
4. (OPTIONAL) If your game is from Steam, Copy [Goldberg](https://gitlab.com/Mr_Goldberg/goldberg_emulator/-/jobs/4247811310/artifacts/download) patch into game directory, make sure to overwrite
5. Run `launch.bat`

## Debug Build Controls

```
Legend:
LCTRL -- Left control.
RCTRL -- Right control.
LALT - Left alt.
RALT - Right alt.
LSHIFT - Left shift
RSHIFT - Right shift.

Main keybinds:
CTRL + TAB -> Switch between game keyboards. Available are debug, marketing, game and replay.

Debug Keybinds:
Backtick ---> Toggle scene information.
Ins (Numpad) ---> Remove debug screen information.
Del (Numpad) ---> Creates a copy of you.
Page up (Numpad) ---> Toggle CPU information.
CTRL + Del (Numpad) ---> Creates a copy of you and sets as your main.
CTRL + Num lock (Numpad) ---> Freezes the game. (literally)
ALT + Enter (Numpad) ---> Fullscreen.

Page up / Page down ---> Change game weather.
Scroll Lock ---> Appears "Streaming paused" message.
Break (Pause break) ---> Freezes the game. (literally)

A ---> Toggle AI display info variants.
B ---> Toggle render info.
D ---> Enable/Disable debug pad.
G ---> Teleport (mouse)
H ---> Health cheat
I ---> Show navmeshes
J ---> Skip to next segment of mission
N ---> Appears your character name in minimap and weird red sphere. (It's AI Walking).
O ---> Toggles minimap on the screen.
Q ---> Changes current character model.
R ---> Navigation info, ambient vehicle info
S ---> Reload shaders
U ---> Spawns a vehicle.
V ---> Invincibility
W ---> Gives a specific amount of all weapons in the game.
X ---> Toggles character clothes info.
Z ---> Mission Debug Menu
F1 ---> Toggle Peds/Cards/Objects/Physics instances and lights info.
F2 ---> AI Combat debug info.
F3 ---> Decrease Wanted Level
F5 ---> Teleports to random location.
F8 ---> FAMILY_CONTROLLER / PLAYER_SWITCH STATE INFORMATION
F9 ---> GAMEFLOW STATE INFORMATION
F10 ---> FRIEND_CONTROLLER STATE INFORMATION
F11 ---> RANDOM EVENTS DEBUG DISPLAY
F12 ---> SCRIPT METRICS DEBUG INFO.

CTRL + A ---> Remove AI display info.
CTRL + B ---> Remove box modifier gui.
LCTRL + C ---> Get all available promotions.
RCTRL + C ---> Show prop hitboxes.
CTRL + D ---> Opens filter menu.
CTRL + F ---> Toggle prop/vehicle information like life ratio.
CTRL + G ---> #UNKNOWN
CTRL + I ---> Toggle mouse relative debug info.
Ctrl + N ---> Show player/vehicle tags.
Ctrl + P ---> Toggle information about promps and show character's hitbox.
Ctrl + T ---> Clear Mission trigger
Ctrl + U ---> Spawns or teleports a vehicle. #PARTIALLYKNOWN
RCTRL + Right/Left arrow key ---> Increase/Decrease timescale.

Ctrl + Shift + C ---> Prop hitboxes.
Ctrl + Shift + H ---> Spawn a human.
Ctrl + Shift + R ---> Init telemetry. #PARTIALLYKNOWN
Ctrl + Shift + P ---> Spawns a car.

ALT + A ---> Toggle vehicle information.
ALT + C ---> Cycle through Camera Debug Displays
ALT + G ---> Change game shader.
ALT + H ---> Toggle shader information.
ALT + M ---> Position zoom.
ALT + O ---> Toggle overdraw info.
ALT + T ---> Toggle texture view gui.
ALT + W ---> Show every prop's hitbox.
ALT + X ---> Removes power cables.

SHIFT/CTRL + B ---> Toggle collision debug info.
SHIFT + H ---> Teleports to your house.
SHIFT + K ---> LowTierGod. (Kills the player.)
SHIFT + O ---> Toggle Overview gui.
SHIFT + P ---> Change characters model in vehicle.
SHIFT + R ---> Toggle peds info.
SHIFT + T ---> Change trigger zone.
SHIFT + U ---> Spawns a vehicle and makes your driver auto.

Ctrl + Alt + I ---> Toggle weapon/inputs information.
```

# Epilogue

Here is the end of the guide, I hope this tutorial was able to help you :)<br>
Some peoples are scaring to share these type of things, i can understand that because they just dont want to get sued.<br>
Just enjoy the game and please star or fork my repository please :3<br>

You can see some screenshots at the bottom about the game.

## Screenshots
![image](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/assets/146978592/bbda2dd9-eb61-482b-a55b-02496440b643)
![image](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/assets/146978592/6441d5d0-6393-41a1-80c1-f1afe8b03119)
![image](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/assets/146978592/c17a2097-13db-49e0-ba4d-b86cec4c74bc)
![image](https://github.com/WH0LEWHALE/gtav-sourcecode-build-guide/assets/146978592/d4ad19d4-b1ce-49f8-a653-b16b70227c93)

## Videos
https://www.youtube.com/watch?v=-RHmcVH4bGQ
https://www.youtube.com/watch?v=n1xav7Mi4KY
https://www.youtube.com/watch?v=TPWWho1cW2Y



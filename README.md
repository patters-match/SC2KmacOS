# SimCity 2000 SE (Win95) on modern macOS

This should be easy, Wine can run Windows software after all. However there are several complications:
- Apple removed 32bit binary support from macOS 10.15 Catalina onwards, so we need to use Wine 64bit which will run the binary in its WOW64
- The SimCity 2000 InstallShield installer is a 16bit executable
- The game has compatibility issues with current Wine 64bit builds (smackw32.dll fails to initialise).
- The game has other issues which need fixing:
  - palette cycling animation issues in >256 colour display modes
  - load/save issues
  - game window initialises at an invisible size

## Wine versions

#### Official ❌
Wine binaries seem to be very scarce. The usual method to install is to use the [brew package manager](https://formulae.brew.sh/cask/wine-stable). However, this 10.02 version (at the time of writing) doesn't seem to work for me for this purpose.

#### CrossOver ❌
[Corbin Davenport's guide](https://www.spacebar.news/how-to-play-simcity-2000-mac/) for the same task I am writing about here had recommended to use [CrossOver](https://www.codeweavers.com/crossover) which is a commercial wrapper around a Wine fork. It offers improvements to Wine, in particular reliable WOW64 support while that was still experimental in Wine. It supports creating multiple Wine configurations or 'bottles' for the specific needs of each Windows software package. It does provide a 14 day trial but I was unable to get it to play SimCity 2000, with the log revealing the reason as smackw32.dll failing to initialise. This bug was reported at Wine 8.0, is confirmed to affect Wine 9.7, and is still open.

#### Porting Kit ✅
I moved onto another method described in [Corbin Davenport's guide](https://www.spacebar.news/how-to-play-simcity-2000-mac/) which is [Porting Kit](https://www.portingkit.com/). It is a free project functionally similar to CrossOver which actually uses the CrossOver forks of Wine, but uses [WineSkin](https://github.com/The-Wineskin-Project/wineskin-source) to manage separate configurations rather than the proprietary 'bottles'. Corbin's guide leaves out the very key detail that we must pick a 64bit Wine engine during setup (which the default is not - perhaps it was different back in 2023). Unfortunately, the recent builds exhibit the same smackw32.dll failure as above.

However, I noted that there are many different engine version selections. I set about finding the newest one which pre-dates the Wine 8.0 issue with smackw32.dll, which turns out to be `WS11WineCX64Bit21.1.0`.

## Installation Steps
- Obtain SimCity 2000 Special Edition for Windows 95
- Extract the WIN95 folder
- Download the [generic 32bit InstallShield 3 EXE](https://community.pcgamingwiki.com/files/file/111-installshield-3-32-bit-generic-installer/) and place it in the WIN95 folder
- 

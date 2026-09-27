# Luma3DS
*Noob-proof (N)3DS "Custom Firmware"*

### What it is
**Luma3DS** is a program to patch the system software of (New) Nintendo (2)3DS handheld consoles "on the fly", adding features such as per-game language settings, debugging capabilities for developers, and removing restrictions enforced by Nintendo such as the region lock.

It also allows you to run unauthorized ("homebrew") content by removing signature checks.
To use it, you will need a console capable of running homebrew software on the Arm9 processor.

Radium3DS's Rosalina menu opens with <kbd>L+Select</kbd> by default; the combo can be changed in Rosalina's Miscellaneous menu.

#
### Compiling
* Prerequisites
    1. git
    2. [makerom](https://github.com/jakcron/Project_CTR) in PATH
    3. [firmtool](https://github.com/TuxSH/firmtool)
    4. Up-to-date devkitARM+libctru
1. Clone the repository with `git clone https://github.com/LumaTeam/Luma3DS.git`
2. Run `make`.

    The produced `boot.firm` is meant to be copied to the root of your SD card for usage with Boot9Strap.

#
### Setup / Usage / Features
See https://github.com/LumaTeam/Luma3DS/wiki

### Supported hardware
Radium3DS currently supports New Nintendo 3DS models only. The ARM9 bootloader checks the hardware model before loading system firmware and displays an error before shutting down on Old Nintendo 3DS models. As this project is open source, this check can be modified in a custom build.

The firmware reports version 14.0.1 in its compatibility metadata and displays the beta label Radium3DS v14.0.1b.

The early ARM9 menu uses the embedded Unscii 8x8 bitmap font by Viznut (public domain / CC0), remapped to preserve CP437 text.

Radium3DS uses a partial install and does not install or update `CTRNAND:/boot.firm`; the CTRNAND copy remains available for returning to vanilla Luma3DS. The early boot configuration menu offers an option to chainload that CTRNAND `boot.firm` for troubleshooting. It clears the option before chainloading, takes effect as soon as the menu is saved, and is only shown when Radium3DS was started from the SD card. The option refuses to chainload a Radium3DS image.

The early boot configuration menu also has a **Boot chainloader** entry for launching payloads from `/luma/payloads`.

### Per-title New 3DS CPU/L2 profiles
The New 3DS Rosalina menu can cycle a CPU/L2 profile for the currently running application. Profiles are saved as a one-byte mode in `/luma/titles/<title ID>/radium3ds_n3ds.bin`; titles without a profile default to 804 MHz and L2 cache enabled. The loader applies the saved profile when starting an application or applet.

The New 3DS menu includes a Super-Stable 3D calibration screen on supported models. Screen filters can apply or restore the IPS-recommended sRGB color curve independently for each screen.

The same menu supports one-to-one swaps among A, B, X, Y, L, R, Start, Select, and the four D-pad directions. Swaps are global and saved in `/luma/radium3ds_buttonmap.bin`; Rosalina loads and applies the saved mapping at startup. C-stick and ZL/ZR remapping are not included.

Rosalina's task manager lists active processes and allows force-closing normal application titles after confirmation. System titles and other non-application processes are protected from this action.

The Rosalina Miscellaneous menu can set Play Coins to the system maximum of 300 by updating Home Menu's shared Play Coin data file.

The notification LED slowly pulses radioactive green by default and resumes its saved on/off state when the console wakes. Its persistent on/off setting is available in Rosalina's Miscellaneous menu.

Rosalina can return to the HOME Menu from its main menu. The System Settings date picker can select years through 2099; the separate NNID birth-year restriction is unchanged.

Rosalina's System info screen reports the top and bottom LCD panel types (IPS/TN when detected), kernel version, MCU firmware, and available hardware vendor data.

#
### Credits
See https://github.com/LumaTeam/Luma3DS/wiki/Credits

#
### Licensing
This software is licensed under the terms of the GPLv3. You can find a copy of the license in the LICENSE.txt file.

Files in the GDB stub are instead triple-licensed as MIT or "GPLv2 or any later version", in which case it's specified in the file header.

# RetroPie on Raspberry Pi Guide
Written by Ayaan Qayyum on 12-25-25

Prerequisites: a computer, Raspberry Pi, and an SD card (at least 32 GB). Ideally a CRT. I will be using a Pi 4 because of the native analog output. 

## Initial Setup
#### 1) Download the correct image for your device at this link: https://retropie.org.uk/download/

#### 2) Flash the image on the SD card with BalenaEtcher. 

#### 3) Boot on the Pi for the first time. 

Just let it do its thing for about five minutes. Then unplug it and plug the SD card into your computer. 

#### 4) Set config files for display output.

Edit the config.txt file to add these at the bottom: 
```
enable_tvout=1

[pi4]
# Disable DRM VC4 V3D driver on Pi 4
dtoverlay=vc4-fkms-v3d

[all]
# overscan_scale=1
# hdmi_force_hotplug=1
# hdmi_group=2
# hdmi_mode=4

gpu_mem=256
dtoverlay=disable-bt

# CRT tweaks
sdtv_mode=0 # Enables NTSC 480i mode. EmulationStation will switch to 240p mode when Retroarch launches.
sdtv_aspect=1 # 4:3 aspect ratio.
disable_overscan=1 # We'll handle overscan on a per-system basis with Retroarch.
audio_pwm_mode=2 # Optional but recommended. Enables an alternative audio driver that works great with the analog audio out.
#framebuffer_width=580 #To properly use this setting you first need to edit out "-yres 448" on "configs/all/runcommand-onstart.sh" and "-yres 480" on "configs/all/runcommand-onend.sh". Optional but recommended if you'll only use a crt tv. Adjust the text of the RetroPie config menus.
#framebuffer_height=360 #To properly use this setting you first need to edit out "-yres 448" on "configs/all/runcommand-onstart.sh" and "-yres 480" on "configs/all/runcommand-onend.sh". Optional but recommended if you'll only use a crt tv. Adjust the text of the RetroPie config menus.
#hdmi_group=1 #Optional. Forces HDMI into 480p mode, useful if you want to emulate a crt tv to test something on an HD display.
#hdmi_mode=2 #Optional. Forces HDMI into 480p mode, useful if you want to emulate a crt tv to test something on an HD display.
hdmi_ignore_hotplug=1 # Optional. Forces composite tv-out even if HDMI is connected.
# overscan_left=16
# overscan_right=16
disable_audio_dither=1
disable_splash=1
```

Restart your Pi and plug in a keyboard or game controller. Now it should boot to the RetroPie GUI. 

## EmulationStation
Now you should be prompted to set up your controller. You have to set up a wired controller at this stage, or even a keyboard. 

The way I play my games, I always set the hotkey key to the left thumbstick since I use it so often. You can also set it to the Start or Select buttons. 

#### 5) Add your games. 

You can set up a USB drive that automatically copies your games to the Pi's internal storage. To set this up, just plug an empty FAT32 formatted drive to the Pi with a folder in the root called `retropie`. It will initialize it for you. Put your games in the folders, including the BIOS files if needed. When you then plug it back into the Pi, it will automatically copy. It's super useful to have a drive that has a flashing LED light for when the drive is being used. That way, you can see that when the LED is done flashing, you can safely unplug the drive.

I made a backup of my RetroPie folder and burned it to a DVD. As I am going through this, I copied the data off the DVD and put it on a freshly formatted drive. 

Once the games are done copying, restart EmulationStation by pressing Start -> Quit -> Restart EmulationStation. All your games should be there. 

#### 6) Bluetooth Controllers

You can set up a controller to be used via Bluetooth. To do this, go to "RetroPie -> Bluetooth -> Pair and Connect to Bluetooth Device". It will search for devices. Whatever device you want to connect, search how to put it in pairing mode for this step. 

For the 8BitDo Pro 2, set the mode to "D" then hold the Start and Sync buttons. The Sync button is at the top of the controller near the USB port. Then select the `Set up udev rule for Joypad`. 

For the DualShock 4, hold the PS button and the Share button (the left one, aka the select button) until the light bar flashes in pulses. 

While the RetroPie is searching for bluetooth devices, you need some device (like a keyboard) to choose it. 

#### 7) Network Connectivity
You can also set network connectivity. This can let you set up network play (which I never used) or copy games over the internet (I personally wouldn't do this).

#### 8) Themes
The default theme is ok but you can set better themes. You can download it directly with wifi or ethernet connectivity. To get to the themes menu, go to the "RetroPie" option on the homepage (where you went to pair a bluetooth controller).

My favorite themes are: 
1. `simpler-turtlemini`
2. `RetroCRT-240p`
3. `retrowave_4_3`

To load this, open Menu -> UI Settings -> Theme Set

People online say that you can copy themes via the USB drive (just how you copied the games), but this did not work for me. Regardless, they say you should add themes to this folder: `retropie/configs/to_retropie/configs/all/emulationstation/themes/`. It should exist but create folders if they don't. Then it should show up. 

You can download the `simpler-turtlemini` from [this link](https://github.com/Omnija/es-theme-simpler-turtlemini).

#### 9) Game Metadata
You can download game metadata by going to Menu -> Scraper. You can have it manually choose the first one by deselecting "User Settles on Conflict". 

## In-Game Config

#### 10) Setting up Rewind & Hotkeys

Rewind is a feature where you can reverse the game and undo your previous moves. To enable it, enter a game. Then open the Quick Menu (Hotkey + X) and turn on Rewind support and configure it. Larger buffer lets you rewind more into the past, and the number of frames changes how fast or sensitive it goes back in time. 

Once it is enabled, press B to enter the Main Menu. Then select Settings -> Input -> Hotkeys. 

I like the following hotkeys: 
```
Fast-Forward (Toggle): Right trigger
Rewind: Left trigger
Load State: Left shoulder
Save State: Right shoulder
```
I also like Confirm Quit being on. 

Once you set it as you like, go to the main menu then pick "Configuration File" then select "Save Current Configuration". I have to set my hotkeys once per console, but I know there's a way to set it for all. 

## Enjoy!

Part of the fun of setting up a RetroPie system is the endless tinkering that is possible. Have fun!
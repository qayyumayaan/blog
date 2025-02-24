# Raspberry Pi Guide Part 2/3: USB Serial
By Ayaan 2-24-25
Part 2/3

So you just got your Linux install. Now what?

The goal of this step is to enable USB Serial, allowing direct communication between your PC and your Pi Zero 2W. You can then SSH into your Pi locally without any dependencies on Wifi. 

**USB Serial Mode** allows you to connect your pi directly to your computer using the second (data) MicroUSB port. 
**"Regular" Mode** is the normal configuration where you can plug in a power source, keyboard, and HDMI and use your Pi as normal. 
One limitation of USB Serial Mode is that you cannot plug in a keyboard and your computer at the same time since it uses the same physical port. You need either a USB to TTL adapter and use the pins or a USB OTG adapter. 

This guide is tailored for enabling USB Serial mode as an option to have. This guide will let you switch between USB Serial mode and Regular Mode. It may not suit your usecase. 

This was tested on Kali Linux, which is based on Debian. Since Raspbian is also based on Debian, it should also work there, but I have not tested it.  

## 1) Disable GUI 
You can change this in `raspi-config`
```bash
sudo systemctl set-default multi-user.target
sudo reboot
```
To reenable GUI on boot, use raspi-config.

To start the GUI in the CLI, run: 
```bash
sudo startx &
```

## 2) (optional) Disable wait for network on boot
```bash
sudo systemctl disable systemd-networkd-wait-online.service
sudo reboot
```

## 3) Enable the getty communication service for USB serial: 
```bash
sudo systemctl restart serial-getty@ttyGS0.service
```

check if it is running with: 
```bash
sudo systemctl status serial-getty@ttyGS0.service
```
It should say enabled in green. 

## 4) Shut down the Pi and edit your `cmdline.txt`: 
Change your `cmdline.txt` to this: 
```bash
console=serial0,115200 console=tty1 root=PARTUUID=fc6ea92b-02 rootfstype=ext4 fsck.repair=yes rootwait modules-load=dwc2,g_serial net.ifnames=0 ds=nocloud cfg80211.ieee80211_regdom=US
```

## 5) Edit your `config.txt`
Add this to the top or bottom of your `config.txt` and ideally remove the rest of the settings that you don't need. Make sure what you already have in your `config.txt` does not conflict with this!

```bash
# SETTINGS FOR USB SERIAL OR REGULAR MODE
# Please enable or disable the other to use a particular mode. 

# ENABLE FOR USB SERIAL
dtoverlay=dwc2
start_x=1

# ENABLE FOR REGULAR MODE
# dr_mode=peripheral

# Lower output resolution to 1/4th of 1080p
framebuffer_width=960
framebuffer_height=540

hdmi_force_hotplug=1
disable_overscan=1
```

# Connecting to your Macbook

It is actually pretty straightforward on a Mac and a headache on Windows. 

## 1) Plug the Micro USB data cable to the second Micro USB port. 
Plug this into your Mac. Having a display is optional. 

## 2) Run the following command on your computer to see if your computer recognizes the Pi: 
```bash
ls /dev/cu.usbmodem*
```

You should see something like this listed: 
```bash
(base) qayyuma@Ayaans-MacBook-Pro ~ % ls /dev/cu.usbmodem*              

/dev/cu.usbmodem11201
```
This Raspberry Pi is identified as `cu.usbmodem11201`. 

## 3) To connect to your Pi, run this command. 
Make sure to change the numbers to match yours.
```bash
screen /dev/cu.usbmodem2101 115200
```

Now it should ask you to connect. Type in `kali`, then `kali` as username and password. 

### Now you are connected to your Pi via USB Serial!
A major limitation is that you cannot directly control the Pi because the one data port is taken up. You need a USB OTG hub for this to work. In order to undo this and be able to run in "normal" mode where you can plug in the power to the power port and plug in a keyboard like normal, you must change your `config.txt` to match this snippet: 


USB Serial Mode: 
```bash
## SETTINGS FOR USB SERIAL OR REGULAR MODE
## Please enable or disable the other to use a particular mode. 

## ENABLE FOR USB SERIAL
dtoverlay=dwc2
start_x=1

## ENABLE FOR REGULAR MODE
## dr_mode=peripheral
```

Regular Mode: 
```bash
## SETTINGS FOR USB SERIAL OR REGULAR MODE
## Please enable or disable the other to use a particular mode. 

## ENABLE FOR USB SERIAL
## dtoverlay=dwc2
## start_x=1

## ENABLE FOR REGULAR MODE
dr_mode=peripheral
```

USB Serial has an identical experience to SSHing over a network. However, there is significantly less lag and you have a lot more free memory. 

## And you're done!
Now you have a Raspberry Pi that you can SSH into locally!
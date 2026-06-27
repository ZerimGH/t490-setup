# t490-setup
My guide for setting up linux on a ThinkPad T490, mainly so I don't forget it

# Touchpad
After installing any distro, I find the touchpad not to be great. Three finger gestures don't work and it generally feels pretty unresponsive.\
I don't exactly know how they work but these kernel parameters make the touchpad feel much better:\
`psmouse.synaptics_intertouch=1`\
`acpi_osi=\"Windows 2015\"`\
If using grub, these should be appended to GRUB_CMDLINE_LINUX_DEFAULT \
\
The generic libinput drivers work fine for me, I don't have an xorg configuration for the touchpad since I'm not on X11, the one shown in https://wiki.archlinux.org/title/Touchpad_Synaptics is a good base.

# Video acceleration
Video acceleration usually doesn't work out of the box for me. Packages libva and intel-media-driver, or the distros equivalent are needed.\
Additionally, on firefox I have to go to about:config and change media.av1.enabled to false, since av1 doesn't work for video acceleration.\
Checking the Video percentage in intel_gpu_top while watching a video can show if hardware acceleration is working or not. If the percentage is at zero, it's using software decoding.

# Undervolting
I don't really notice a difference when undervolting, but it's still nice to have.\
I've used both throttled and intel-undervolt for undervolting, both work just fine.\
The offsets I've found to be safe for me are -85mV on CPU and CPU cache, and -105mV on the GPU, maybe I could push it further but I've never had crashes with these offsets.

# Font rendering
This one isn't specific to the T490, but I still want to mention it here since it's such a great change.\
\
https://github.com/maximilionus/lucidglyph  
This script very noticeably improved the clarity of fonts, things feel much sharper and easier to read.\
\
https://www.reddit.com/r/linux_gaming/comments/16lwgnj/is_it_possible_to_improve_font_rendering_on_linux/
From the top comment here, appending FREETYPE_PROPERTIES="cff:no-stem-darkening=0 autofitter:no-stem-darkening=0" to /etc/environment seems to help too.

# Firmware update
Updating firmware is usually a good idea, especially if you bought an old laptop second-hand\
Lenovo do firmware updates through the fwupd utility, install it with your package manager and run `fwupdmgr update` in the terminal. I'm not sure how safe doing this is, but nothing's broken for me. After next reboot it will apply the changes, you should probably make sure the laptop doesn't die while updating.

# BIOS options
I haven't touched the bios much, all I would recommend doing is disabling secure boot, allowing legacy boot if you need it, disable any CPU features you don't want.\
I also disabled the keyboard beep and the WWAN card in the security page somewhere. The beep annoys me, and disabling the WWAN card for whatever reason makes it wake from sleep much faster.

# Thermal stuff
I don't know how much of a difference it makes, but intel have a daemon called thermald which is meant to help prevent overheating. I haven't noticed a difference with it on or off, the thermals in this laptop are pretty bad tbh.\
Theres also thinkfan which I've never set up, it gives you control over the fan speed which may be useful if the laptop is overheating or the fans are running loud when they shouldn't be.

# Battery
I use tlp to manage power profiles and charging thresholds. You can configure it to use a profile to save power when the laptop isn't plugged in, and also to stop and start charging at some percentage of full capacity which is good for battery health.

# Fingerprints
Fingerprints on linux kinda suck from what I've seen \
These are some useful pages for getting it set up \
https://wiki.archlinux.org/title/Fprint \
https://wiki.archlinux.org/title/SDDM#Using_a_fingerprint_reader \
This repo helped get fingerprint working with SDDM the way I think it should
https://github.com/xCaptaiN09/sddm-fingerprint

# (Very specific) Minecraft 1.16
In Minecraft version 1.16 and maybe some later versions too, for whatever reason inputs are quite buggy. I assume it's because of the laptop's keyboard's rollover and grouping and stuff.\
Changing the LWJGL version to one higher than the default for that version fixed it for whatever reason.
\
\
\
If I have any other problems that I find a solution to, or think of anything I haven't mentioned, I'll add them here :)

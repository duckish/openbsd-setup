

###The first thing to do is disable the annoying xconsole window from autostarting at each login. We'll also disable the system beep in the session manager.

sed -i 's/xconsole/#xconsole/' /etc/X11/xenodm/Xsetup_0
echo 'xset b off' >> /etc/X11/xenodm/Xsetup_0


##You can also disable the beep when logged into a virtual console, as well as remap Caps Lock to the Control key, by editing /etc/wsconsctl.conf



usermod -G staff YOUR_USERNAME


mkdir -p ~/.config/gtk-3.0

## to install and update firmwure, check if firmware is loaded correctly 
dmesg | grep iwm

## look at this page :

https://www.openbsd.org/faq/faq4.html

and find section :

Bootstrapping Wireless Firmware

## run these commands with doas

doas ifconfig iwm0 -wpakey
doas ifconfig iwm0 nwid eduroam wpa wpaakms 802.1x up
doas wpa_supplicant -Bc /etc/wpa_supplicant.conf -D openbsd -i iwm0
doas dhclient iwm0

## for home
doas ifconfig iwm0 nwid "VIDEOTRON3468_5GHz" wpakey "xxxxxxxxxxxxx"
doas dhclient iwm0


### check if usb headphone is connected 

doas dmesg | grep uaudio

## we should see something like :

uaudio0 at uhub0 port 2 configuration 1 interface 1 "Sennheiser Sennheiser SC 1x5 USB" rev 2.00/0.18 addr 6
uaudio0: class v1, full-speed, sync, channels: 2 play, 2 rec, 7 ctls
audio1 at uaudio0

## Programs will use snd/default, which points to snd/0, by default. This binding can be quickly changed using server.device like so: 

sndioctl server.device=1 

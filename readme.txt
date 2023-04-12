

###The first thing to do is disable the annoying xconsole window from autostarting at each login. We'll also disable the system beep in the session manager.

sed -i 's/xconsole/#xconsole/' /etc/X11/xenodm/Xsetup_0
echo 'xset b off' >> /etc/X11/xenodm/Xsetup_0


##You can also disable the beep when logged into a virtual console, as well as remap Caps Lock to the Control key, by editing /etc/wsconsctl.conf



usermod -G staff YOUR_USERNAME


mkdir -p ~/.config/gtk-3.0
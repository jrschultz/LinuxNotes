# Post Install Steps for Fedora (Gnome)

## Update the system

sudo dnf5 upgrade

## Tweak DNF Config

sudo nvim /etc/dnf/dnf.conf 

Add:

max_parallel_downloads=10

## Update Firmware

```
sudo fwupdmgr refresh --force

sudo fwupdmgr get-updates

sudo fwupdmgr update
```

## Enable RPM Fusion

Copy the command from [this website](https://rpmfusion.org/Configuration)

## Update after RPM Fusion 

sudo dnf5 upgrade

## Install Gnome Tweaks

sudo dnf5 install gnome-tweaks

## Enable Flathub for Flatpaks

Copy the command from [this website](https://flathub.org/setup/Fedora)

## Install Gnome Extensions

Search it in the Software Store

## Install Apps

sudo dnf5 install vlc mpv p7zip p7zip-plugins unrar pandoc texlive-scheme-full 



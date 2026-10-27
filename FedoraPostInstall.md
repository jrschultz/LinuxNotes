# 🎩 Post Install Steps for Fedora (Gnome)

## Update the system

```bash
sudo dnf5 upgrade
```

## Tweak DNF Config

```bash
sudo nvim /etc/dnf/dnf.conf
```

Add:

```bash
max_parallel_downloads=10
```

## Update Firmware

```bash
sudo fwupdmgr refresh --force

sudo fwupdmgr get-updates

sudo fwupdmgr update
```

## Enable RPM Fusion

Copy the command from [this website](https://rpmfusion.org/Configuration)

## Update after RPM Fusion 

```bash
sudo dnf5 upgrade
```

## Install Gnome Tweaks

```bash
sudo dnf5 install gnome-tweaks
```

## Enable Flathub for Flatpaks

Copy the command from [this website](https://flathub.org/setup/Fedora)

## Install Gnome Extensions

Search it in the Software Store

## Install Apps

```bash
sudo dnf5 install vlc mpv p7zip p7zip-plugins unrar pandoc texlive-scheme-full 
```


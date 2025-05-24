# Archinstall Update

To update archinstall only from the installer:

pacman -S archinstall

If that fails, you may need:

pacman -Sy pacman -S archlinux-keyring pacman -S archinstall

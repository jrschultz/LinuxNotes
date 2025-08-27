# Fixing the Scanner on Arch Linux

## Update Arch

```
sudo pacman -Syu
```

## Groups Setup

```
sudo usermod -G scanner -a jason
```

```
sudo gpasswd -a jason scanner
```

## Kernel Module

You need the kernel module ```sg``` - this should be loaded by default but mine wasn't.

I reinstalled the kernel

``` 
sudo pacman -S linux
```

Then I rebuilt intramfs and rebooted

```
sudo mkinitcpio -P && sudo reboot
```

### Manually Load sg

```
sudo modprobe sg
```

### Install Packages

```
sudo pacman -S sane
```
```
yay -S libsane-dsseries 1.0.5_1-2
```

### Document Scanner

Document Scanner App should now detect the scanner

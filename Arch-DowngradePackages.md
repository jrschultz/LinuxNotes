# Downgrading a package on Arch Linux

Sometimes stuff breaks.

## Find the Offender

Narrow down what isn't working and then search for it:

```bash
ls /var/cache/pacman/pkg | grep -i cups
```

Identify the offending package and then downgrade to the previous version in the package cache.

```bash
sudo pacman -U /var/cache/pacman/pkg/libcups-2:2.4.14-1-x86_64.pkg.tar.zst
```

You just swap out the offending package for what is ailing the system

## Made it Stick

If you upgrade, it will just undo your downgrade.

```bash
sudo nvim /etc/pacman.conf
```

And scroll down to this line and add your held packages.

```bash
IgnorePkg = cups libcups
```

If the program is from the AUR, you simply reinstall the AUR package with a clean build. You should not use the above holding method for AUR stuff.

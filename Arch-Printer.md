# Setting up the Brother HL-L2320D Printer

## Update Arch

```
sudo pacman -Syu
```

## Install cups

```
sudo pacman -S cups
```

## Enable the Printing Service

```
sudo systemctl enable --now cups
```

## Install from AUR

```
yay install brlaser
```
## Add the Printer

From the cups web dialogue add the printer using the brlaser driver option


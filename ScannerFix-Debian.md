# Scanner fix in Debian 13 on

### Brother DSmobile 620 Scanner

When you force-install a package with dpkg, the Debian package manager (apt) flags it as "broken" because its old dependencies (like the legacy libsane) are not met in Debian 13. To fix this permanently so it doesn't revert during updates, you must satisfy the dependency system using one of the following methods.

### Method 1: Create a "Fake" Dependency Package (Recommended)
This is the cleanest 2026 solution. You create a tiny "dummy" package that tells Debian "I have libsane installed," which satisfies the Brother driver without actually changing your system libraries. 
Install the ```equivs``` tool:

```bash
sudo apt update && sudo apt install equivs
```

Generate a control file:
```bash
equivs-control libsane
```

Edit the file:
Open the generated libsane file in a text editor. Change the following lines:

```Package: libsane```

```Version: 1.0.99 (Use a high version to ensure it satisfies all requirements)```

```Description: Dummy package for legacy Brother scanner drivers```

Build and install:

```bash
equivs-build libsane
```

```bash
sudo dpkg -i libsane_1.0.99_all.deb
```

Re-install the Brother driver:

Now you can install the driver normally without --force-all:

```bash
sudo apt install ./libsane-dsseries_1.0.5-1_amd64.deb
```

Then do this:

```bash
sudo usermod -G scanner -a jason && sudo gpasswd -a jason scanner
```

This adds the user to the scanner group and viola!

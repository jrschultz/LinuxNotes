# 📂 ZFS Cheat Sheet & Setup Guide

A comprehensive reference guide for managing ZFS pools, disks, quotas, permissions, and maintenance on Ubuntu.

---

## 🚀 Installation on Ubuntu

Get started by installing the core ZFS utilities and viewing system info:

```bash
sudo apt install zfsutils-linux
```

> 💡 **ZFS on Root:** If you want to boot from ZFS, also install the initramfs package:
> ```bash
> sudo apt install zfs-initramfs
> ```

Check your system storage info with:
```bash
df -h
```

---

## 🏊 Pool Management

### Create a Pool
```bash
zpool create [Name of pool] [what kind] disk1 disk2
```
*Example:*
```bash
zpool create BigPool mirror disk1 disk2
```

### Add Devices to a Pool
```bash
zpool add BigPool mirror disk3 disk4
```

### Check Status
```bash
zpool status
```

### Segment / Partition a Pool (Datasets)
```bash
zfs create BigPool/data
zfs create BigPool/apps
```

### Destroy / Take Apart a Pool
```bash
zpool destroy BigPool
```
> ⚠️ **Note:** You may need to export the pool first. If it has trouble unmounting, ensure nothing is connected to it and that no shell is currently open in that directory.
> ```bash
> sudo zpool export [POOLNAME]
> ```

---

## 🛡️ RAID Options & Configuration

### Supported RAID Levels
* **Mirror** 🪞 (Data mirrored across drives)
* **Raidz1** ⚙️ (Equivalent to RAID 5, tolerates 1 drive failure)
* **Raidz2** ⚙️ (Equivalent to RAID 6, tolerates 2 drive failures)
* **Raidz3** ⚙️ (Tolerates 3 drive failures)

### Creating a RAID Pool
```bash
zpool create BigPool raidz disk1 disk2 disk3 disk4
```

> 🔑 **Best Practice:** Create pools using stable device IDs (like serial numbers) instead of generic names like `/dev/sda` to prevent naming shifts after reboots.
> 
> Check UUIDs/IDs:
> ```bash
> ls -la /dev/disk/by-uuid/
> ```
> 
> Example creation with stable disk paths:
> ```bash
> sudo zpool create [POOLNAME] raidz1 /dev/disk/by-id/ata-HGST345k34j4
> ```

---

## 🔧 Hardware Diagnostics & Disk Replacement

### Locate a Bad Disk
```bash
sudo hdparm -I /dev/sd?
```
Or filter by serial number using `grep`:
```bash
sudo hdparm -I /dev/sd? | grep 'Serial'
```

### Replace a Bad Disk in a Pool
```bash
zpool replace -f BigPool disk4 disk9
```
> * `-f`: Forces the replacement if data is already present.

### Take a Bad Disk Offline
```bash
zpool offline BigPool disk8
```

### Bring a Disk Back Online (Re-add)
```bash
zpool online BigPool disk8
```

---

## 📊 Quotas, Space & Permissions

### Setting Quotas
Set a strict logical ceiling on a dataset (can be changed anytime since it's a logical volume, not physical):
```bash
zfs set quota=100M BigPool/data/jacob
```

### Reserving Space
Reserve guaranteed space for a user or dataset:
```bash
zfs set reservation=100M BigPool/data/matthew
```

### Inspect Dataset Settings
```bash
zfs get all BigPool/data
```

### Changing Permissions
```bash
sudo chown -R [USERNAME] /[ZPOOL]
```

---

## 🌐 Sharing via Samba

Enable SMB sharing on a ZFS dataset:
```bash
sudo zfs set sharesmb=on [POOLNAME/FOLDER]
```

Ensure the user is added to the Samba server on the OS (note: the Samba password must match their Linux login password):
```bash
sudo smbpasswd -a USERNAME
```

---

## 🛠️ Maintenance & Scrubbing

* **Verify and Fix Checksums:**
  ```bash
  sudo zpool scrub jcloud
  ```
  *(Verifies all checksums and automatically attempts to fix corrupted files).*

* **Stop a Running Scrub:**
  ```bash
  zpool scrub -s myPool
  ```
  *(Scrubs can take a long time; use this if you need to abort).*

---

## 📝 My Recommended ZFS Setup Steps

1. **Install Utilities:**
   ```bash
   sudo apt install zfsutils-linux
   ```
2. **Create the Pool with Advanced Formatting:**
   ```bash
   sudo zpool create jcloud -f -o ashift=12 raidz1 /dev/sdb /dev/sdc /dev/sdd ...
   ```
   * `-f`: Forces creation even if data is present.
   * `-o ashift=12`: Advanced format for modern disks (post-2011), using 4096-byte sectors.
3. **Export the Pool:**
   ```bash
   zpool export jcloud
   ```
4. **Re-import Using Unique Disk IDs:**
   ```bash
   zpool import jcloud -d /dev/disk/by-id
   ```
   *(Ensures the pool maps to persistent disk identifiers instead of generic `/dev/sdX` labels).*
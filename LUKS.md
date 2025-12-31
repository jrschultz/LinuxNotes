# LUKS Setup for Full Drive Encryption

You need sudo/root to do the following steps

## Install package from your repo

```
cryptsetup
``` 

## Locate your drive to encrypt

```bash
lsblk
```

## Prepare the Drive with fdisk

```bash
fdisk /dev/sdd
```

Follow the fdisk prompts to delete any old partitions and make a new one. Generally **d,n,p,Y,w**

## Create the Encryption on Desired Partition

```bash
cryptsetup luksFormat /dev/sdd1
```

It will ask to confirm overwriting the data. Then it will ask for your passphrase. This will be what you use to decrypt and open the partition.

## Open the Encrypted Partition

```bash
cryptsetup open /dev/sdd1 cuda2tb
```

where 'cuda2tb' is what you want to call the drive

It will ask for your passphrase.

You can check to see if this worked with 

```bash
lsblk
```

Your encrypted partition should show up under sdd1

## Create Filesystem

The encrypted partition needs a file system. You only need to do this setup once.

```bash
mkfs.ext4 /dev/mapper/cuda2tb
``` 

## Mount the Partition for Use

```bash
mount /dev/mapper/cuda2tb /mnt/cuda2tb
```

You can now copy or create data on the encrypted partition as per any other hard drive.

## Unmount and Close Procedure

When you are done with the drive follow these steps.

### Run Sync

Sync will write any buffered file system data

```bash
sync
```

### Unmount

```bash
umount /mnt/cuda2tb
```

### Close the Encrypted Partition

Closing the partition locks it and prevents viewing it.

```bash
cryptsetup close cuda2tb
```

# Everyday Use Commands Once Setup

## Open (Decrypt)

```bash
cryptsetup open /dev/sdd1 cuda2tb
```

Enter the passphrase.

## Mount 

```bash
mount /dev/mapper/cuda2tb /mnt/cuda2tb
```

## Use Drive as Needed

## Unmount

```bash
umount /mnt/cuda2tb
```

## Close (Encrypt)

```bash
cryptsetup close cuda2tb
``` 












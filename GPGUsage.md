# GPG Guide

GnuPG (GNU Privacy Guard) is an open-source implementation of the OpenPGP standard, used for secure communication and data protection.

The basic features are **encrypting data & verifying authenticity.** 

## Generate a Key

The most modern and efficient key type is ECDH with Curve25519.

```
gpg --expert --full-gen-key
```

Select 9 ```ECC and ECC```

Select 1 ```Curve25519```

Choose how long you want the key to remain active, ex: 3y

Finish creating the key with name & email, etc. details.

### Verify the Key

```
gpg --list-keys
```

Sample output:

```
pub   ed25519 2025-05-31 [SC]
      A1B2C3D4E5F6G7H8
uid           [ultimate] John Doe <john@example.com>
sub   cv25519 2025-05-31 [E]
```

## Exporting Keys

### Sharing a Public Key

```
gpg --armor --export A1B2C3D4E5F6G7H8 > public-key.asc
```

You can upload this to a [Key Server](keys.openpgp.org)

```
gpg --send-keys A1B2C3D4E5F6G7H8
```

### Backing Up a Private Key

**NEVER publicly share your private key.**

```
gpg --armor --export-secret-keys A1B2C3D4E5F6G7H8 > private-key.asc
```

## Importing Keys

### Importing from a file

```
gpg --import public-key.asc
```

### Importing from a key server

```
gpg --recv-keys <key-id>
```

### Trust a key to verify signatures

```
gpg --edit-key <key-id>
gpg> trust
```

You can set the trust level to 5 for ultimate trust.

## Encrypting Data

### Encrypt a file for a recipient (using that person's public key)

```
gpg --encrypt --recipient <recipient-key-id> file.txt
```

This outputs 

```
file.txt.gpg
```

### Multiple Recipients

```
gpg --encrypt --recipient <key-id1> --recipient <key-id2> file.txt
```

### Symmetric Encryption

This doesn't use keys. It uses a passphrase. Fine for local storage.

```
gpg --symmetric file.txt
```

### Type an Encrypted Message

```
echo "This is my secret message" | gpg --encrypt --armor --recipient B1C2D3E4F5G6H7I8 > message.asc
```

+ Use the echo command to type your message
+ Pipe it to GPG recipient 
+ ```>``` exports it to a an encrypted file

## Decrypting Data

Using your private key and passphrase.

```
gpg --decrypt file.txt.gpg > file.txt
```

This will prompt for a passphrase.

## Signing Data

### Signing a File
Signing a file proves it came from you.

```
gpg --sign file.txt
```

Outputs: 

```
file.txt.gpg
```

### Detached Signature

This creates a separate .sig file

```
gpg --detach-sign file.txt
```

Outputs: 

```
file.txt.sig
```

### Clear Sign

Creates a human readable signature

```
gpg --clearsign file.txt
```

Outputs:

```
file.txt.asc
```

### Verifying Signatures

Verify a signed file

```
gpg --verify file.txt.gpg
```

Verify a detached signature

```
gpg --verify file.txt.sig file.txt
```

## Key Management

### List Keys

```
gpg --list-keys
```

### Revoke a Key

```
gpg --gen-revoke A1B2C3D4E5F6G7H8 > revoke.asc
```

Then

```
gpg --import revoke.asc
gpg --send-keys A1B2C3D4E5F6G7H8
```



    










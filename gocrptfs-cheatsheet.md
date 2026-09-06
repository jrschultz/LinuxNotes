## Make folders
```bash
mkdir myfiles_encrypted myfiles_decrypted
```

## Initialize Encryption
```bash
gocryptfs -init myfiles_encrypted
```

## mount folders
```bash
gocryptfs myfiles_encrypted myfiles_decrypted
```

## unmount/lock folder
```bash
fusermount -u myfiles_decrypted
```

## using master key
```bash
gocryptfs -masterkey=stdin myfiles_encrypted myfiles_decrypted
```
or [clear it from history after]
```bash
gocryptfs -masterkey=YOUR-MASTER-KEY-HERE myfiles_encrypted myfiles_decrypted
```

## reset password
```bash
gocryptfs -passwd -masterkey=stdin myfiles_encrypted
```

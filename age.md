**age** (Actually Good Encryption) is a simple, modern, and secure file encryption tool. It uses small explicit keys, has almost no options to get wrong, and works well with Unix pipes. Official site: [age-encryption.org](age-encryption.org).

# 🪄 KEY GENERATION

### ✅ Classic X25519 key (recommended for most use)
```bash
age-keygen -o key.txt
```

Ex: Public key: age1ql3z7hjy54pw3hyww5ayyfg7zqgvc7w3j2elw8zmrj2kg5sfn9aqmcac8p


### 🐈‍⬛ Post-quantum hybrid (ML-KEM-768 + X25519) — recommended for long-term security
```bash
age-keygen -pq -o key.txt
```

Public key starts with age1pq1... (very long, ~2000 chars)

### Extract public key from an identity file
```bash
age-keygen -y key.txt
```

### Encrypt the private key itself with a passphrase
``` bash
age-keygen | age -p > key.age
```

Keep the private key (AGE-SECRET-KEY-...) secret. Share only the public key (age1... or age1pq1...).

# 🔐 BASIC USAGE

## 🔓 Symmetric Encryption (No Keys Needed)

### Encrypt (leave empty to auto-generate a strong passphrase)
```bash
age -p -o secrets.txt.age secrets.txt
```

### Decrypt
```bash
age -d -o secrets.txt secrets.txt.age
```

## 🔑🔑 Asymmetric Encryption (Public Key Encryption)

### Encrypt to one recipient
``` bash
age -r age{RECIPIENT KEY} -o file.age file.txt
```

### Decrypt
``` bash
age -d -i key.txt -o file.txt file.age
```

### Multiple recipients (any one can decrypt)
You can keep recipient key list in a text file, one per line, '#' comments are ignored.

```
# Alice
age1ql3z7hjy54pw3hyww5ayyfg7zqgvc7w3j2elw8zmrj2kg5sfn9aqmcac8p
# Bob
age1lggyhqrw2nlhcxprm67z43rta597azn8gknawjehu9d9dl0jq3yqqvfafg
```

```bash
age -R recipients.txt -o shared.age file.txt
```

### ASCII Armour - Text format for email/chat

```bash
age -a -r age1... -o message.age message.txt
# or to stdout
age -a -p < message.txt
```

## 🤫 SSH Keys

SSH keys work (ssh-ed25519 and ssh-rsa ≥ 2048), but native age keys are preferred (smaller, better privacy, post-quantum available). ssh-agent is not supported.


### Encrypt to an SSH public key
```bash
age -R ~/.ssh/id_ed25519.pub -o file.age file.txt
```

### Decrypt with the private key
```bash
age -d -i ~/.ssh/id_ed25519 -o file.txt file.age
```

### Encrypt to a GitHub user’s keys
```bash
curl https://github.com/username.keys | age -R - -o file.age file.txt
```

# ⚙️ COMMON OPTIONS

| **Flag** | **Description** |
| -------- | --------------- |
| -e / --encrypt | Encrypt (default) |
| -d / --decrypt | Decrypt |
| -o FILE | Write output to file (default: stdout) |
| -a / --armor | ASCII-armored output |
| -p / --passphrase | Encrypt with a passphrase |
| -r RECIPIENT | Encrypt to a public key (repeatable) |
| -R FILE | Read recipients from a file |
| -i FILE | Identity (private key) file for decryption |


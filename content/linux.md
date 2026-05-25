---
publish: true
title: 🐧 Linux
created: 2026-01-29T21:35:21.000+01:00
modified: 2026-04-11T14:33:52.695+02:00
tags:
  - Tech/OS/Linux
---

# Commands

## 🔢 Base64

**Encode text:** `echo -n '<gh-username>:<gh-access-token>' | base64`

**Decode text:** `echo -n 'PGdoLXVzZXJuYW1lPjo8Z2gtYWNjZXNzLXRva2VuPg==' | base64 -d`

## 📋 Copy to Clipboard

You can copy any output directly to your clipboard with:

`echo 'something' | pbcopy`: (Simply append `| pbcopy` to any command to copy its output automatically.)

## Delete folder

`rm -rf <folderName`

## Resource usage

- `htop` → Live Ressourcen-Monitor mit Terminal-Grafik (muss ggf. installiert werden)
- `free -h` → Zeigt die Ressourcen zum Zeitpunkt der Befehlausführung an (nativ, kann bei Memory teilweise ungenau sein, vor allem bei Shared-VPS)
- `df -h` → Zeigt die Speicherbenutzung an (nativ)

## List applications

- Shows applications which listens on several ports: `sudo lsof -i -P -n`
- Shows application which listens on a specific port: `sudo lsof -i -P -n | grep :80`

# Generate key

- Generate Secure random string
  ```Bash
  # 128 is the length of the string
  cat /dev/urandom | LC_ALL=C tr -dc 'a-zA-Z0-9' | fold -w 128 | head -n 1

  # 32 is the length of the string
  openssl rand -base64 64 | head -c 32; echo
  ```

## Path escaping

Add before the space a backslash (’`\`’)

```Bash
# From
mv /Users/mattiamueggler/Documents/Schule/3. Lehrjahr/1. Semester/M122/node/testApi /Users/mattiamueggler/Documents/Projects/node/

# To
mv /Users/mattiamueggler/Documents/Schule/3.\ Lehrjahr/1.\ Semester/M122/node/testApi /Users/mattiamueggler/Documents/Projects/node/
```

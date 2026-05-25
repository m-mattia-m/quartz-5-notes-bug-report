---
publish: true
aliases:
  - How to use certificates
title: How to use certificates
created: 2026-01-29T21:35:13.000+01:00
modified: 2026-01-29T21:35:13.000+01:00
tags:
  - Tech/Security/Certificates
---

> ℹ️ To get my certificates check out [[my-certificates]]

## How to use my provided keys

### RSA

> Notice that the size is **limited** to 501 Bytes.

1. Safe your message in a file. `echo "Hi, this is my encrypted message" >> message.txt`
2. Encrypt this file and convert it to an base64 encoded text. `openssl rsautl -encrypt -inkey mattiamueggler_public_key.pem -pubin -in message.txt -out encrypted_message.bin && base64 -i encrypted_message.bin >> encrypted_message.txt`
3. Print the encoded value from your file. `cat encrypted_message.txt`
4. _Send me either the value of this base64 encoded file or the file directly._

### PGP

1. Install [GnuPG](https://gnupg.org/)
2. Import the public key from another person with: `gpg --import mattia-at-mattiamueggler-ch_public.key`
3. Safe your message in a file. `echo "Hi, this is my encrypted message" >> message.txt`
4. Encrypt the file by the mail your key is generated for: `gpg -e -r mattia@mattiamueggler.ch -o encrypted_output.txt message.txt`
5. _Send me either the value of this base64 encoded file or the file directly._

### S/MIME

You don’t need to encrypt your message manually, like before. Download my certificate and add it to your keychain. (If I wrote you a mail before from my email address, your mail client probably stored my certificate automatically on your keychain.)

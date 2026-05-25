---
publish: true
aliases:
  - How to generate a RSA key
title: How to generate a RSA key
created: 2026-01-29T21:35:11.000+01:00
modified: 2026-04-11T16:19:41.372+02:00
tags:
  - Tech/Security/Certificates
---

## Generation

> [!important] I have my own public and private key but this is for creating a new one if it’s necessary.

1. create privat key which is encrypted stored with a passphrase: `openssl genpkey -algorithm RSA -out mattiamueggler_private_key.pem -aes-256-cbc -pass pass:my-passphrase` → generates a encrypted private key in the current directory with the passphrase `my-passphrase`
2. generate a public key from the private key (you have to enter your private key): `openssl rsa -pubout -in mattiamueggler_private_key.pem -out mattiamueggler_public_key.pem`

## Encrypt message

> [!important] Notice that the size is **limited** to 501 Bytes.

1. create message: `echo "Hi, this is my encrypted message" >> message.txt`
2. encrypt message/file and convert encrypted message to base64 encoded text: `openssl rsautl -encrypt -inkey mattiamueggler_public_key.pem -pubin -in message.txt -out encrypted_message.bin && base64 -i encrypted_message.bin >> encrypted_message.txt`
3. return base64 encoded message: `cat encrypted_message.txt`
4. _do what you want with this message._

## Decrypt message

1. save base64 encoded text to a file: `echo "SGVsbG8gV29ybGQK" >> base64.txt` (base64: `Hello World`)
2. decode base64 encoded text: `base64 -d -i base64.txt > encoded.bin`
3. encrypt message with private key (you have to enter your passphrase for your private key): `openssl rsautl -decrypt -inkey mattiamueggler_private_key.pem -in encoded.bin -out decrypted_message.txt`

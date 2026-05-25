---
publish: true
aliases:
  - How to generate a PGP key
title: How to generate a PGP key
created: 2026-01-29T21:35:11.000+01:00
modified: 2026-04-11T16:26:01.123+02:00
tags:
  - Tech/Security/Certificates
---

At the beginning the have to clarify what it PGP, GPG, OpenPGP:

- **PGP**: Pretty Good Privacy → Asymmetric encryption to encrypt files, messages, mails, …
- **OpenPGP**: GNU Privacy Guard → OpenSource version of PGP
- **GPG**: Open Pretty Good Privacy → UI (User Interface (→ CLI)) for PGP

---

## Generation

> [!important] You have to **refresh** your key before it expires. (on all key-servers, your website like [mattiamueggler.ch](mattiamueggler.ch), locally, 1Password and every place you store it).

1. [Install CLI tool](https://gnupg.org/) → `brew install gnupg`
2. Generate key with: `gpg --full-generate-key`
   1. Select encryption type → `RSA and RSA`
   2. bit-length → `4096`
   3. expire date → `2y` (why: [No expiry for offline primary PGP key?](https://security.stackexchange.com/questions/239608/no-expiry-for-offline-primary-pgp-key))
   4. Real name → `Mattia Müggler`
   5. Email address → `mattia@mattiamueggler.ch`
   6. Comment → `-`
   7. add a passphrase → `asdfasdf12345` (use something secure)
3. export public key: `gpg -a --export mattia@mattiamueggler.ch > mattia-at-mattiamueggler-ch_public.key`
4. export private key: `gpg -a --export-secret-keys mattia@mattiamueggler.ch > mattia-at-mattiamueggler-ch_private.key`

## Encrypt

1. Import the public key from another person with: `gpg --import mattia-at-mattiamueggler-ch_public.key`
2. Create a file you want to encrypt: `echo "content" >> message.txt`
3. Encrypt the file by the mail your key is generated for: `gpg -e -r mattia@mattiamueggler.ch -o encrypted_output.txt message.txt`
4. If there is an error, you have to add the public key to your keychain.

## Decrypt

1. Check if your private key is installed: `gpg --list-secret-keys`
   1. if not use `gpg --import private-key.key` to import it
2. Decrypt your file: `gpg -d -o decrypred_message.txt encrypted_output.txt`
3. Type your passphrase if this is demanded.
4. If there is an error, you have to add the private key to your keychain.

## Revoke key

> Creates a certificate which you can use to revoke a key in the future for some reasons.

1. `gpg --output revocation.crt --gen-revoke mattia@mattiamueggler.ch`
   1. Select the reason for the revocation → `No reason specified`
   2. Description → `-`

## Refresh key

> Your token must be refreshed before it expires.

1. refresh token with: `gpg --refresh-keys`
2. upload it to all places where you share your public key like:
   - 1Password
   - [mattiamueggler.ch](http://mattiamueggler.ch)
   - key-servers (if you have one → at the moment I haven’t shared it on one)

## Sign Key

> This tells your software/device that you trust this key. This is useful for persons you are sure for 100% that this person is who he tells he is. You can ensure if this person is who he tells he is through fingerprints (if you are not sitting next to them :)).

1. Sign a public key from another person with: `gpg --sign-key email@example.com`

## Key servers

You can share your public key with the WWW because the design of the key ensures that nothing nasty could be happen with your public key ([Source](https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages#how-to-make-your-public-key-highly-available)). You can upload it to your website or share it on a key server, but you have to maintain your key if this expires.

### Famous key servers

- [keys.openpgp.org](https://keys.openpgp.org/)
- [pgp.mit.edu](http://pgp.mit.edu/)
- [certserver.pgp.com](http://certserver.pgp.com/)
- Provide your own `.well-known` endpoint on your domain (OpenPGP | [Web Key Directory](https://www.ietf.org/archive/id/draft-koch-openpgp-webkey-service-18.html))
-

## Mail Integration

You can use [GPGTools](https://gpgtools.org/) ([official “recommended” from Apple](https://gpgtools.tenderapp.com/kb/gpg-mail-faq/how-to-enable-gpg-mail-on-macos)) to integrate it in apple mail.

1. Open Mail
2. Mail › Settings › Extensions
3. Click on the checkbox next to GPG Mail

## Sources

- https://gist.github.com/Lukas238/e23989749995257f23812b4042c53309
- https://www.metanet.ch/de/email/sicherheit/verschluesselung/pgp
- https://pgpkeygen.com/
  - Could also be generated on this platform but you can not ensure that they not save your key pair.
- https://security.stackexchange.com/questions/239608/no-expiry-for-offline-primary-pgp-key
- https://www.goanywhere.com/blog/openpgp-pgp-gpg-whats-the-difference
- https://www.redhat.com/sysadmin/encryption-decryption-gpg
- https://www.tecmint.com/gpg-encrypt-decrypt-files/
- https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages
- https://gpgtools.com/sonoma

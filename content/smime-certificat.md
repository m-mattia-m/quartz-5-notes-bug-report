---
publish: true
aliases:
  - S/MIME-Certificate
  - S/MIME
title: S/MIME-Certificate
created: 2026-01-29T21:35:20.000+01:00
modified: 2026-03-15T20:37:59.727+01:00
tags:
  - Tech/Security/Certificates
---

# Generation

I’ve bough on [WISeID a Personal Certificate](https://wiseid.com/pricing/). After the payment I could request one. I’ve had to add a passphrase and then I could generate one. After that I was able to download a certificate and a certificate combined with the private key. I stored this file (cert with private key) in 1Password by the “Webmail - Main” element.

# Setting up

## Mac

Then I double-clicked on the certificate with the private key and import it to my keychain.

## iPhone and iPad

I downloaded the cert (with the private key) to my files folder and open it. My device asked me on which device I want to install the certificate/profile. I selected my device iPhone/iPad and then I went to my system settings and open the profile tab. There I selected the new certificate/profile and installed it (I had to type my passphrase). After I’ve added this cert I went to my Mail-Settings → Accounts → \<select the account with the provides email in the certificate> → Account settings → Advanced → (s/MIME) Sign = YES, Encrypt by Default = YES (and select for each option your added certificate)

# Expiration

You can say during the payment how long the certificate should be valid (1-3 years) after this period of time you have to replace your certificate with a new one. For this you have to buy a new certificate and import this to all your devices and remove the old one. But notice if you remove your old one you can’t read the mails from earlier anymore so you better add an additional certificate.

# Publishing

You can publish it on a DNS record which is standardized. Therefore you can create a SMIMEA [[DNS]] record and provided there your public certificate for the domain your certificate is issued.

- [What is a SMIMEA record? Secure Email with S/MIME](https://www.cloudns.net/wiki/article/386/)

---

## Sources

- https://wiseid.com/pricing/
- https://account.wiseid.com/dashboard/digital?type=advanced
- https://support.apple.com/de-ch/guide/mail/mlhlp1179/mac

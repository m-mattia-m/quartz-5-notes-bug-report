---
publish: true
created: 2026-01-29T21:35:20.000+01:00
modified: 2026-04-11T13:22:03.423+02:00
tags:
  - Tech/Network
---

```Bash
# fqdn: tsa.pki.admin.ch
# port: 443
echo >/dev/tcp/tsa.pki.admin.ch/443&&  echo "connection is open"

# fqdn: tsa.pki.admin.ch
nslookup tsa.pki.admin.ch

# fqdn: tsa.pki.admin.ch
dig tsa.pki.admin.ch

# fqdn: tsa.pki.admin.ch
# port: 443
nc -zv tsa.pki.admin.ch 443
```

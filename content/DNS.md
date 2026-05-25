---
publish: true
title: DNS
created: 2026-01-29T21:35:22.000+01:00
modified: 2026-02-16T22:13:05.487+01:00
tags:
  - Tech/Network
---

# General

#TODO

# Control external DNS

If you should control an external DNS entry but you don't have access to this DNS you can ask them if they can create the DNS record and point to one of yours DNS records. Then you can update your DNS record and point to a new target. For example if you are hosting an application for a company and you don't want that they have to care about server migrations.

```
# My own record
A :: k8s.own-domain.tld -> <K8s-IPv4>

# external record
CNAME :: tool.external-domain.tld -> k8s.own-domain.tld
```

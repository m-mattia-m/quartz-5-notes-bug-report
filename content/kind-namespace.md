---
publish: true
aliases:
  - Namespace
title: "Kind: Namespace"
created: 2026-01-29T21:35:20.000+01:00
modified: 2026-02-24T13:18:58.986+01:00
tags:
  - Tech/DevOps/Kubernetes/Kinds
---

# Namespace

Ist ein Projekt in K8s. Verschiedene Namespaces werden durch ein K8s-Netztwerk von einander getrennt, kann jedoch wie eine Firewall geöffnet werden.

# How to create a Namespace?

1. Melde dich beim K8s-Dashboard an
2. Gehe oben rechts auf das `+`
3. Erstelle ein Namespace via “**Create from input”**
   ```yaml
   apiVersion: v1
   Kind: Namespace
   metadata:
     name: <namespace-name>
   ```
4. upload the file

# Example

```yaml
apiVersion: v1
Kind: Namespace
metadata:
  name: test-api
```

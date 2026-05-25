---
publish: true
aliases:
  - Secret
title: "Kind: Secret"
created: 2026-01-29T21:35:20.000+01:00
modified: 2026-02-24T13:18:58.981+01:00
tags:
  - Tech/DevOps/Kubernetes/Kinds
---

```yaml
# Here you can create Secrets for Formtion which will be passed on as Environment.

apiVersion: v1
Kind: Secret
metadata:
  name: test-api-secrets
  namespace: test-api
data:
  TEST_SECRET: YXNkZi10ZXN0LXNlY3JldA== # asdf-test-secret
```

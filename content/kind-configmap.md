---
publish: true
aliases:
  - ConfigMap
title: "Kind: ConfigMap"
created: 2026-02-07T12:23:58.000+01:00
modified: 2026-02-24T13:18:58.960+01:00
tags:
  - Tech/DevOps/Kubernetes/Kinds
---

```yaml
# here a file is created which can importet in the deployment

apiVersion: v1
Kind: ConfigMap
metadata:
  name: test-api-file
  namespace: test-api
data:
  file.txt: |-
    This is the file value.
```

---
publish: true
title: SealedSecret generation
created: 2026-01-29T21:35:12.000+01:00
modified: 2026-02-16T22:15:23.401+01:00
tags:
  - Tech/Security
  - Tech/DevOps/Kubernetes
---

# How to check in secrets in Git

Since you want to check in some secrets in your Git repository as a DevOps approach. However, you don't want to have a #Tech/Security  issue with storing them in plaintext or just [[linux#Base64]] encoded. Therefore you can encrypt the whole [[kind-secret|Secret]] with seal. Consider that just the cluster where the sealSecret-controller is installed can decrypt it. Also you have to store it in the correct namespace

```bash
oc create secret generic my-secret-name \
  --from-literal=git-token='<TOKEN-HERE>' \
  --dry-run=client -o yaml \
  -n target-namespace | kubeseal -w my-secret-name.yaml \
  --controller-namespace operator-sealed-secrets \
  --controller-name sealed-secrets-controller \
  -o yaml \
  -n target-namespace
  
# Customize:
# my-secret-name -> Name of the secret
# git-token -> Name of the key
# <TOKEN-HERE> -> Value for the key above
# target-namespace -> your namespace where the secret should be stored
# my-secret-name.yaml -> local file name where the secret is stored
```

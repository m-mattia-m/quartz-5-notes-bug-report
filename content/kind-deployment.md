---
publish: true
aliases:
  - Deployment
title: "Kind: Deployment"
created: 2026-01-29T21:35:20.000+01:00
modified: 2026-02-24T13:18:58.960+01:00
tags:
  - Tech/DevOps/Kubernetes/Kinds
---

# When to use Deployment

Deployments are designed to be Stateless, so if it doesn't matter if you kill a pod it just starts another one. You can also scale horizontally so it doesn't matter how many instances you have in parallel. If you will have a state or can't just have several instances next to each other, check out [[kind-statefulSets|StatefulSet]]

# Example

```yaml
# Here the application itself is created

apiVersion: apps/v1
Kind: Deployment
metadata:
  name: test-api
  namespace: test-api
spec:
  replicas: 1
  selector:
    matchLabels:
      app: test-api
  template:
    metadata:
      labels:
        app: test-api
		    # app.kubernetes.io/name: test-api
    spec:
      imagePullSecrets:
        - name: ghcr-pull-secret
      containers:
        - name: test-api
          image: ghcr.io/mattiamueggler/test-api:v1.0.6
          env:
            - name: TEST_ENV
              value: "asdf-test-env"
            - name: TEST_SECRET
              valueFrom:
                secretKeyRef:
                  name: test-api-secrets
                  key: TEST_SECRET
          volumeMounts:
            - name: file-volume
              mountPath: /config/file.txt
              subPath: file.txt
      volumes:
        - name: file-volume
          configMap: 
            name: test-api-file
            items: 
              - key: file.txt
                path: file.txt
```

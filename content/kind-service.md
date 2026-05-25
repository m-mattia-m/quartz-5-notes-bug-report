---
publish: true
aliases:
  - Service
title: "Kind: Service"
created: 2026-01-29T21:35:20.000+01:00
modified: 2026-02-24T13:18:58.976+01:00
tags:
  - Tech/DevOps/Kubernetes/Kinds
---

# What is a Service?

Gibt eine App im Namespace, da eine Applikation (in einem Pod) jeweils für sich selbst läuft, damit die Applikation (Pods) in einem Namespace miteinander Kommunizieren können müssen diese via Service geöffnet werden. In diesem Service kann man den Service-Namen definieren und auch den Input & Output-Port, aber auch das Protokoll.

# Example

```yaml
# here is the service-creation to expose the app in the namespace

apiVersion: v1
Kind: Service
metadata:
  name: test-api
  namespace: test-api
spec:
  selector:
    app: test-api
  ports:
    - name: http
      port: 80
      targetPort: 8080
```

## Pod selector

Damit der Service auf den richtigen Pod connecten kann, muss der `selector` und das `label`
übereinstimmen. Wenn beim Deployment das `label` `app` benutzt wird muss beim Service auch der `selector` `app` benutzt werden. Ansonsten muss bei beiden `app.kubernetes.io/name` benutzt werden, jedoch müssen beide immer die selben sein.

```yaml
# Deployment
spec.template.metadata.labels:
	app: fiduciary-crm-frontend

# Service
spec.selector:
	app: fiduciary-crm-frontend
```

## Inter-Cluster-traffic

- `<serviceName>.<namespaceName>.svc.cluster.local`
- `<serviceName>.svc.cluster.local`

[Kubernetes - internal DNS service](https://www.rancher.com/docs/rancher/v1.2/en/kubernetes/k8s-internal-dns-service/)

---
publish: true
aliases:
  - Ingress
title: "Kind: Ingress"
created: 2026-01-29T21:35:20.000+01:00
modified: 2026-02-24T13:18:58.971+01:00
tags:
  - Tech/DevOps/Kubernetes/Kinds
---

# What is an Ingress?

Verbindet das Internet zum Services und handelt auch die Verschlüsselung. Hier kann entweder ein eigenes Zertifikat pro Namespace hineingeladen werden oder ein Wire…-Zertifikate welches für alle Namespaces vom ganzen K8s her gilt.

# Example

```yaml
# here is the route-creation to expose the app-service to the internet

apiVersion: networking.k8s.io/v1
Kind: Ingress
metadata:
  name: test-api
  namespace: test-api
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-nginx
spec:
  rules:
  - host: test-api.formtion.app
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: test-api
            port:
              number: 80
  ingressClassName: nginx
```

# With TLS-Certificate

## Issuer → Certificate generation

Use for trobleshooting the staging-Issuer, because the prod-issuer has a strict rate-limit.

```yaml
apiVersion: cert-manager.io/v1
Kind: ClusterIssuer
metadata:
  name: letsencrypt-staging
spec:
  acme:
    # The ACME server URL
    server: https://acme-staging-v02.api.letsencrypt.org/directory
    # Email address used for ACME registration
    email: user@example.com
    # Name of a secret used to store the ACME account private key
    privateKeySecretRef:
      name: letsencrypt-staging
    # Enable the HTTP-01 challenge provider
    solvers:
      - http01:
          ingress:
            ingressClassName: nginx



apiVersion: cert-manager.io/v1
Kind: ClusterIssuer
metadata:
  name: letsencrypt-prod
spec:
  acme:
    # The ACME server URL
    server: https://acme-v02.api.letsencrypt.org/directory
    # Email address used for ACME registration
    email: user@example.com
    # Name of a secret used to store the ACME account private key
    privateKeySecretRef:
      name: letsencrypt-prod
    # Enable the HTTP-01 challenge provider
    solvers:
      - http01:
          ingress:
            ingressClassName: nginx
```

## Ingress

```yaml
apiVersion: networking.k8s.io/v1
Kind: Ingress
metadata:
  name: fiduciary-crm-backend
  namespace: kuratli-fiduciary-crm
  annotations:
    cert-manager.io/cluster-issuer: "letsencrypt-staging" # letsencrypt-prod
spec:
  ingressClassName: nginx
  tls:
  - hosts:
    - crm-api.makefermion.com
    secretName: fiduciary-crm-backend-tls # will be automatically created 
  rules:
  - host: crm-api.makefermion.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: kuratli-fiduciary-crm-backend
            port:
              number: 80
```

https://cert-manager.io/docs/tutorials/acme/nginx-ingress/
https://cert-manager.io/docs/troubleshooting/

Wenn kein Certifacte ausgestellt wird, kann man die Events im Certificate ansehen:

`kubectl describe certificate <cert-name> -n <your-namespace>` \
(`kubectl get certificate -n <your-namespace>`)

Hier kommen die Meldungen warum kein Certificate ausgestellt wird. Wenn hier nichts relevantes steht, kann man im cert-manager-namespace die Pods neu starten. Bevor die Pods gestartet werden muss sichergestellt werden dass die Issuer für den aktuellen Namespace bestehen (sieht man ob die Issuer Zertifikate in den Secrets haben → falls nicht vorhanden anlegen). In den meisten fällen sollte man aber in den Events etwas sehen wie z.B. dass zu viele Zertifikate ausgestellt wurden und aktuell gewartet werden muss.

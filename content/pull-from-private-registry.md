---
publish: true
title: Pull from a private registry
created: 2026-01-29T21:35:10.000+01:00
modified: 2026-02-24T13:18:58.959+01:00
tags:
  - Tech/DevOps/Kubernetes
---

# How to pull an image from a private registry

Sometimes, you need to access an image stored in a private registry, such as **ghcr.io**, which requires authentication.

1. Log in to the registry `docker login ghcr.io -u <gh-username> -p <access-token>`
2. Locate your Docker config file: the configuration is usually stored in `~/.docker/config.json`. If it doesn’t exist, you can create it manually:
   ```json
   {
   	"auths": {
   		"ghcr.io": {},
   	}
   }
   ```
3. Add the `auth` attribute to the registry entry: The value must be a base64-encoded string of `"username:password"`.
   ```json
   {
   	"auths": {
   		"ghcr.io": {
   			"auth": "dXNlcm5hbWU6cGFzc3dvcmQ=" // value from `echo -n 'username:password' | base64`
   		}
   	}
   }
   ```
4. Encode the entire file in base64: `cat config.json | base64`
5. Create a [[Kubernetes|Kubernetes]] Secret using the encoded config: Save the base64-encoded value in a Secret manifest:
   ```yaml
   apiVersion: v1
   Kind: Secret
   type: kubernetes.io/dockerconfigjson
   metadata:
   	name: ghcr-pull-secret
   	namespace: formtion
   data:
     .dockerconfigjson: <base64-encoded-config-file> # set here your base64 encoded config.json
   ```
6. save the manifest `kubectl apply -f ghcr-pull-secret.yaml`

# Source

- [kubernetes.io - pull from private registry](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)

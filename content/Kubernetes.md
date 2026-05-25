---
publish: true
aliases:
  - K8s
title: ⚙️ Kubernetes
created: 2026-01-29T21:35:21.000+01:00
modified: 2026-03-06T21:55:44.862+01:00
tags:
  - Tech/DevOps/Kubernetes
---

# ❓ What is Kubernetes \[K8s]

**Kubernetes**, often abbreviated as **K8s**, is an open-source platform for container orchestration. It enables efficient deployment, management, and scaling of containerized applications. K8s automates tasks such as load balancing, resource allocation, and container self-healing, which improves application availability and scalability.

It is based on a **declarative configuration model**, allowing developers and operators to define the desired state of their applications instead of executing manual steps. K8s also provides a rich ecosystem of tools and resources for container orchestration and has become a key technology in **cloud-native development**.

# Navigation

- [[Kind]]
- [[inter-pod-communication|Inter-Pod-Kommunikation]]
- [[pull-from-private-registry|Pull from a private registry]]
- [[Nodes]]
- [[Operator]]
- [[Resources]]
- [[sealed-secret-generation|SealedSecret generation]]
- [[sidecar-containers|Sidecar Containers]]

# Manifests

```dataview
LIST WITHOUT ID "[[" + file.path + "|" + file.frontmatter.title + "]]"
FROM #Tech/DevOps/Kubernetes/Kinds 
SORT file.frontmatter.title ASC
```

# 🕹️ Playground

- [play-with-k8s: labs (online)](https://labs.play-with-k8s.com/)
- [minikube (local)](https://minikube.sigs.k8s.io/docs/)
- [kind (local)](https://kind.sigs.k8s.io/)

# Contribute to Kubernetes

- [Kubernetes Community](https://github.com/kubernetes/community/)
- [Kubernetes contribution overview](https://github.com/kubernetes/community/tree/master/contributors/devel#readme)
- [Developer Guide - How to contribute](https://github.com/kubernetes/community/tree/master/contributors/guide)

# ℹ️ Help / Tutorials

- [cloudytuts.com](https://www.cloudytuts.com/tutorials/kubernetes/)

---

## Sources

- [DigitalOcean - An Introduction To Kubernetes](https://www.digitalocean.com/community/tutorials/an-introduction-to-kubernetes)
- [DigitalOcean - Infrastructure Best Practices](https://docs.digitalocean.com/developer-center/digitalocean-kubernetes-infrastructure-best-practices/)
- [Kubernetes](https://www.cloudytuts.com/tutorials/kubernetes/)
- [prefetch.net](https://prefetch.net/blog/2019/10/16/the-beginners-guide-to-creating-kubernetes-manifests/)
- [schoenwald.aero](https://schoenwald.aero/posts/2025-02-24_introduction-to-kubernetes/)

---
publish: true
title: Components
created: 2026-01-29T21:35:21.000+01:00
modified: 2026-01-29T21:35:21.000+01:00
tags:
  - Tech/DevOps/Kubernetes
---

# Glossar

| **Name**                 | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Node**                 | A machine on which Kubernetes runs (either a physical or virtual server).<br><br>**Master / Control Plane:**<br>The master nodes are responsible for managing the Kubernetes control plane. They coordinate the cluster, provide the Kubernetes API, and handle all core management tasks.<br><br>**Worker Nodes:**<br>The worker nodes run the deployed applications and their associated resources.                                        |
| **Cluster**              | A cluster is a group of nodes that work together to provide high availability and fault tolerance in case one node fails.                                                                                                                                                                                                                                                                                                                    |
| **Namespace**            | A namespace is like a project in Kubernetes. Different namespaces are isolated from each other at the network level but can communicate if explicitly allowed (similar to a firewall rule). It serves as a logical grouping for applications and resources.                                                                                                                                                                                  |
| **Service (Networking)** | A Service is a networking component that allows different Pods to communicate with each other and with the outside world. You can define input and output ports, as well as the communication protocol.                                                                                                                                                                                                                                      |
| **Ingress Controller**   | An Ingress Controller manages external access to Services within a cluster. It acts as a load balancer that distributes traffic across multiple Pods and handles routing based on defined Ingress rules. It also serves as a reverse proxy that manages TLS certificates and encryption. Having a proxy in front of the load balancer is a common setup in production environments.                                                          |
| **Ingress (Networking)** | An Ingress manages inbound HTTP(S) traffic to Services. You can define an FQDN, configure encryption (TLS), and specify routing rules to forward traffic to the appropriate Service.                                                                                                                                                                                                                                                         |
| **Pod**                  | The smallest deployable unit in Kubernetes — a Pod runs one or more containers that share the same network and storage. <br><br>**Init Container:**<br>Runs before the main container to perform setup tasks, such as database migrations. It stops once the initialization is complete.<br><br>**Sidecar Container:**<br>Runs alongside the main container to handle supporting tasks, such as logging, synchronization, or scheduled jobs. |

# Sources

- [DigitalOcean](https://docs.digitalocean.com/developer-center/digitalocean-kubernetes-infrastructure-best-practices/)
- [Spacelift.io](https://spacelift.io/blog/statefulset-vs-deployment)

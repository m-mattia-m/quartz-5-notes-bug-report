---
publish: true
aliases:
  - kubectl
title: kubectl
created: 2026-01-29T21:35:21.000+01:00
modified: 2026-01-29T21:35:21.000+01:00
tags:
  - Tech/DevOps/Kubernetes
---

# Extensions

Install [Kubecolor](https://kubecolor.github.io/)for a colorful terminal. Add this config to the [[zsh]] config:

```bash
# kubectl
source <(kubectl completion zsh) # enables autocompletion for kubectl
alias k=kubectl # shortcut for kubectl
alias kubectl="kubecolor" # use kubecolor instead of kubectl
alias kx="kubectx" # shortcut for context switch
alias kn="kubens" # shortcut for namespace switch
alias oc="env KUBECTL_COMMAND=oc kubecolor" # use oc (openshift) with kubecolor
export KUBECOLOR_PRESET="deuteranopia-dark" # set the kubecolor theme
compdef kubecolor=kubectl # replaces kubectl with kubecolor
```

# Installation

## kubecolor

Works with `kubectl` and `oc` → use `deuteranopia-dark`-theme.

> `brew install kubecolor`

[kubecolor.github.io](https://kubecolor.github.io/)

## kubectl

> `brew install kubernetes-cli`

[brew.sh](https://formulae.brew.sh/formula/kubernetes-cli)

## oc

> `brew install openshift-cli`

[brew.sh](https://formulae.brew.sh/formula/openshift-cli)

# Getting started

Before you can use the CLI, you need to have access to the cluster you want to manage. To connect to it, you must save the kubecontext in your kubeconfig file. Add the context to the configuration file located at `~/.kube/config`.

- **Via CLI:** `doctl kubernetes cluster kubeconfig save <clusterId>`
- **Manually:** `nano ~/.kube/config` → copy the kubeconfig into the config file
- **Verify:** `cat ~/.kube/config`

[kubernetes.io - MacOS installation](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/#install-with-homebrew-on-macos)

# Usage

`k <verb> <resource> ...` \
`-o <output: yaml/json/wide>` \
`-f <file-path>` (for apply) \
`-n <namespace>`for a specific one or `-A` for all namespaces

## Verbs

- `get`
- `describe`
- `apply`
- `edit` (edit resource with `vi`)
- ...

## Resources

- `pod`
- `service` or `svc`
- `ingress`
- `namespace` or `ns`
- `configmap` or `cm`
- ...

# Advanced

## Delete all pods with specific state

```bash
kubectl get pod -n <namespace> | grep <Status> | awk '{print $1}' | xargs kubectl delete pod -n <namespace> 
kubectl get pod -n zitadel | grep ContainerStatusUnknown | awk '{print $1}' | xargs kubectl delete pod -n zitadel 

# for several states and define the namespace just once 
NAMESPACE=<namespace> && kubectl get pods -n "$NAMESPACE" --no-headers | grep -E 'Completed|Evicted|PodInitializing|Error|ContainerStatusUnknown' | awk '{print $1}' | xargs -r kubectl delete pod -n "$NAMESPACE"
```

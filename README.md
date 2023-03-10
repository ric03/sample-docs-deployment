# Simple Docs Deployment

This repo contains the deployment config (Helm Chart) for the
app [sample-docs-app](https://github.com/ric03/sample-docs-app).

This repo is part of an ArgoCD experiment, see https://github.com/ric03/sample-docs-argocd

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/ric03/sample-docs-argocd/raw/main/docs/component-overview-transparent-darkmode.png">
  <img alt="Component Overview" src="https://github.com/ric03/sample-docs-argocd/raw/main/docs/component-overview-transparent.png">
</picture>

# Requirements

- kubectl
- kubens (optional)
- helm
- Kubernetes Cluster (e.g. locally with [kind](https://kind.sigs.k8s.io/))

# Some Commands

Generate the k8s objects

```shell
helm template my-app .
```

If you have access to a k8s-cluster, you can install the app

```shell
helm install my-app . -n playground
```

The service type is set to `NodePort`, the installation command will print
the commands to get the ip and port to access the app.

```shell
export NODE_PORT=$(kubectl get --namespace playground -o jsonpath="{.spec.ports[0].nodePort}" services local-test-sample-docs-deployment)
export NODE_IP=$(kubectl get nodes --namespace playground -o jsonpath="{.items[0].status.addresses[0].address}")
echo http://$NODE_IP:$NODE_PORT
```

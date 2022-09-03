# Argo CD

Declarative continuous delivery with a fully-loaded UI.

## references

[ArgoCD Documentation](https://argo-cd.readthedocs.io/en/stable/)

## usage

In order to access the server UI you have the following options:

1. Retrieve the initial admin password

```sh
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d; echo
```

1. create a port forward to the argocd-service and then open the browser on http://localhost:8080 and accept the certificate

```sh
kubectl port-forward service/argocd-server -n argocd 8080:443
```

(You should delete the initial secret afterwards as suggested by the Getting Started Guide: https://github.com/argoproj/argo-cd/blob/master/docs/getting_started.md#4-login-using-the-cli)

## install cli tool

```sh
make cli
```

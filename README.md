# "Hello World" of Argo + Crossplane

This repo is designed to be the simplist possible example of getting a trivial Crossplane control plane running with Helm. 

## Instructions

Assuming you have a kubernetes running (kind works)

```shell
$ kubectl create namespace argocd
$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

$ kubectl apply -f argocd/configmap.yaml

$ brew install argocd
$ argocd login --core
$ argocd admin initial-password -n argocd

$ kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Login to https://localhost:8080/, change password, and re-login

In a new tab:

```shell
$ kubectl apply -f argocd/crossplane.yaml

## Get your creds however works for you (rippling)
$ kubectl create secret generic aws-secret -n crossplane-system --from-file=creds=/tmp/aws.cred

 
$ kubectl apply -f argocd/xp-app.yaml 

```
# argocd-gitops-example
This repository is used as part of a gitops deployment strategy with tekton and Minikube.

- [argocd tutorial](https://redhat-scholars.github.io/argocd-tutorial/argocd-tutorial/01-setup.html)
- [argocd getting started](https://argo-cd.readthedocs.io/en/stable/getting_started/)

## Useful commands
#### ArgoCD
- `minikube start`
- `kubectl create namespace argocd`
- `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
- `brew install argocd`
- `kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'`
- `kubectl port-forward svc/argocd-server -n argocd 8080:443`
- `argocd admin initial-password -n argocd`
- `argocd login localhost:8080`

#### Tekton
- `kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml`
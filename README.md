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
- `minikube start --memory 6144 --cpus 2`
- `eval $(minikube -p minikube docker-env)`
- `minikube addons enable registry`
- `minikube addons enable registry-aliases`
- `kubectl version --short` (check if kubectl is connected to minikube; `short` will be removed in the future)
- `brew install tektoncd-cli` (install tekton cli) or
  - `choco install tektoncd-cli --confirm` or
  - `https://github.com/tektoncd/cli/releases`
- `kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml` (install tekton pipeline)
- `kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/release.yaml` (install tekton triggers)
- `kubectl get pods --namespace tekton-pipelines --watch` (check if tekton is running)
- `tkn hub install task git-clone` (install git-clone task from tekton hub)
- `tkn task list` (list all tasks - to check if git-clone is installed)
- `kubectl apply -f show-readme.yml` (apply the show-readme task)
- `tkn task start show-readme --dry-run` (optional - dry run the show-readme task)
- `kubectl apply -f pipeline.yml` (apply the pipeline)
- `kubectl create -f pipelinerun.yml` (create the pipeline run)
  - This creates a PipelineRun resource with a unique name and a reference to the Pipeline resource to run. e.g. `pipelinerun.tekton.dev/clone-read-run-4kgjr`
- `kubectl get pipelinerun` (get the pipeline run)
- `tkn pipelinerun logs  clone-read-run-4kgjr -f` (get the logs of the pipeline run, change the name to the name of your pipeline run)
- `kubectl get tasks` (get all tasks)
- `kubectl get taskruns` (get all task runs)
- `kubectl get pipelineruns` (get all pipeline runs)
- `minikube delete --all` (delete all resources)

#### TODO - look into setting up git-credentials secrets for tekton correctly

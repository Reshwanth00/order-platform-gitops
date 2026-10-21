# Order platform GitOps

Kustomize manifests for the local Kubernetes learning environment. Before use, replace `YOUR_DOCKERHUB_USER` in `overlays/local/kustomization.yaml` and `YOUR_GIT_REPO_URL` in `argocd/application.yaml`.

```sh
kubectl apply -k overlays/local
kubectl -n order-platform get pods,svc
kubectl -n order-platform port-forward svc/frontend 3000:80
```

Argo CD can manage this repository by applying `argocd/application.yaml` after updating its repository URL. CI builds and pushes immutable build-number tags; update the image tag in the overlay as a Git commit to trigger reconciliation.

# Order platform GitOps

Kustomize manifests for the local Kubernetes learning environment. For Docker Desktop Kubernetes, use the local image overlay. For a remote cluster, replace `YOUR_DOCKERHUB_USER` in `overlays/local/kustomization.yaml` and push images to that registry.

```sh
kubectl apply -k overlays/docker-desktop
kubectl -n order-platform get pods,svc
kubectl -n order-platform port-forward svc/frontend 3000:80
```

Build the three images first from the application repo with `docker compose build order-service catalog-service frontend`. The overlay points Kubernetes at those local Docker Desktop images.

Argo CD can manage this repository by applying `argocd/application.yaml` after updating its repository URL. CI builds and pushes immutable build-number tags; update the image tag in the overlay as a Git commit to trigger reconciliation.

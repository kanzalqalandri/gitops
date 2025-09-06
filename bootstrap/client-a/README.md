# add repo
helm repo add argo https://argoproj.github.io/argo-helm
kubectl create namespace argocd

# install Argo CD with client-specific values
helm upgrade --install argocd argo/argo-cd \
  --namespace argocd \
  --version 8.3.1 \
  -f bootstrap/dnv-infradev/argocd-values.yaml

# install root app
kubectl apply -f bootstrap/dnv-infradev/root-application.yaml

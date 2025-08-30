# add repo and create ns
helm repo add argo https://argoproj.github.io/argo-helm
kubectl create namespace argocd --dry-run=client -o yaml | kubectl apply -f -

# install Argo CD with client-specific values
helm upgrade --install argocd argo/argo-cd \
  --namespace argocd \
  --version 6.6.0 \
  -f bootstrap/client-a/argocd-values.yaml

# install root app
kubectl apply -f clusters/client-a/bootstrap/root-application.yaml

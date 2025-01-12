cd ~/iCloud/Homelab/git/homelab-foss
kubectl create ns argocd || true
kubens argocd
kubectl apply -k ./src/argocd/bootstrap-resources/argocd
kubectl apply -f ~/iCloud/keys/k8s/k8s.prd.yml
kubectl apply -f ./src/argocd/cluster-bootstrap.yml

# Add ArgoCD OIDC:
kubectl patch configmap argocd-cm --patch-file ~/iCloud/keys/k8s/argocd-oidc-cm.yml
kubectl patch secret argocd-secret --patch-file ~/iCloud/keys/k8s/argocd-oidc-secret.yml
kubectl patch configmap argocd-rbac-cm --patch-file ~/iCloud/keys/k8s/argocd-oidc-rbac-cm.yml
kubectl rollout restart deployment argocd-server

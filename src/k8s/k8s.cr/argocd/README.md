cd ~/iCloud/Homelab/git/homelab-foss
kubectl create ns argocd || true
kubens argocd
kubectl apply -k src/k8s/k8s.cr/argocd/resources/argocd
kubectl apply -f ~/iCloud/keys/k8s/k8s.prd.yml
kubectl apply -f ./src/k8s/k8s.cr/argocd/cluster-apps.yml

# Add ArgoCD OIDC:
kubectl patch configmap argocd-cm --patch-file ~/iCloud/keys/k8s/argocd-oidc-cm.yml
kubectl patch secret argocd-secret --patch-file ~/iCloud/keys/k8s/argocd-oidc-secret.yml
kubectl patch configmap argocd-rbac-cm --patch-file ~/iCloud/keys/k8s/argocd-oidc-rbac-cm.yml
kubectl rollout restart deployment argocd-server

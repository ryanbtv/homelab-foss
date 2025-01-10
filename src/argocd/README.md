cd ~/iCloud/Homelab/git/homelab-foss
kubectl create ns argocd || true
kubens argocd
kubectl apply -k ./src/argocd/bootstrap-resources/argocd
kubectl apply -f ~/iCloud/keys/sealed-secrets/k8s.prod/backup.yml
kubectl apply -f ./src/argocd/cluster-bootstrap.yml
kubectl apply -f ./argocd/cluster-apps.yml

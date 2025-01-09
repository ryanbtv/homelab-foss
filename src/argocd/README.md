cd ~/iCloud/Homelab/git/homelab-foss
kubectl create ns argocd || true
kubens argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.13.3/manifests/ha/install.yaml
kubectl apply -k ./src/argocd/bootstrap-resources/argocd/kustomization.yml
# kubectl apply -n argocd -f ./src/argocd/bootstrap-resources/argocd/appproj.yml
kubectl apply -f ./src/argocd/cluster-bootstrap.yml
kubectl apply -f ./argocd/cluster-apps.yml

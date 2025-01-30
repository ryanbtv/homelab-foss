Create cluster from existing secret data:

``` bash
# Set the current Talos config to our iCloud-backed version
export TALOS_NAME='k8s.cr'
export TALOS_NODE='10.1.60.11'

talosctl gen config -e $TALOS_NODE ${TALOS_NAME} "https://${TALOS_NAME}.ff.lan:6443" --output "src/k8s/${TALOS_NAME}/talos/.configs"

# Merge src/k8s/${TALOS_NAME}/talos/.configs/talosconfig into the main talosconfig source
talosctl config remove $TALOS_NAME # If you have an existing config to overwrite
talosctl config merge "src/k8s/${TALOS_NAME}/talos/.configs/talosconfig" # Merge this talosconfig into your main one
talosctl config endpoint $TALOS_NODE
talosctl config node $TALOS_NODE

# Apply Node Configs
talosctl apply-config --insecure --nodes $TALOS_NODE --file "src/k8s/${TALOS_NAME}/talos/.configs/controlplane.yaml" --config-patch @"src/k8s/${TALOS_NAME}/talos/patch.controlplane.yml" --config-patch @"src/k8s/${TALOS_NAME}/talos/patch.common.yml"

talosctl bootstrap -n $TALOS_NODE -e $TALOS_NODE

# Once done and all nodes are up, you can grab the kubeconfig and bring it local:
talosctl kubeconfig ~/iCloud/Homelab/kubeconfig.yml --force-context-name $TALOS_NAME -n $TALOS_NODE -e $TALOS_NODE --force-context-name $TALOS_NAME

# add this kubeconfig to the existing $KUBECONFIG env var if needed
code ~/.zshrc
```



/Users/ryanb/Library/Mobile Documents/com~apple~CloudDocs/Homelab/git/homelab-foss
/Users/ryanb/iCloud/Homelab/kubeconfigs
/Users/ryanb/Library/Mobile Documents/com~apple~CloudDocs/Homelab/kubeconfigs
/Users/ryanb/Library/Mobile Documents/com~apple~CloudDocs/


```    registries:
        config:
            registry-1.docker.io:
                auth:
                    username: slothcroissant
                    password: ^U%/ZRq1H0oU

talosctl -e 10.1.40.10 --nodes 10.1.40.11 --nodes 10.1.40.12 --nodes 10.1.40.13 --nodes 10.1.40.14 --nodes 10.1.40.15 --nodes 10.1.40.16 --nodes 10.1.40.17 --nodes 10.1.40.18 edit machineconfig

# Apply Node Configs (after cluster creation)
talosctl apply-config -e 10.1.40.10 --nodes 10.1.40.11 --nodes 10.1.40.12 --nodes 10.1.40.13 --nodes 10.1.40.14 --file src/k8s/${TALOS_NAME}/talos/.configs/controlplane.yaml --config-patch @src/k8s/${TALOS_NAME}/talos/patch.controlplane.yml --config-patch @src/k8s/${TALOS_NAME}/talos/patch.common.yml
talosctl apply-config -e 10.1.40.10 --nodes 10.1.40.15 --nodes 10.1.40.16 --nodes 10.1.40.17 --nodes 10.1.40.18 --file src/k8s/${TALOS_NAME}/talos/.configs/worker.yaml --config-patch @src/k8s/${TALOS_NAME}/talos/patch.common.yml
```
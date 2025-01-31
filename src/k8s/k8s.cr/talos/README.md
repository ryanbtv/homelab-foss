Create cluster from existing secret data:

``` bash
# Set the current Talos config to our iCloud-backed version
export TALOS_NAME='k8s.cr'
export TALOS_NODE='10.1.40.31'

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

```
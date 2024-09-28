# Install Flux 

Doc: 

``` bash
flux bootstrap git \
  --url=ssh://git@github.com/ryanbtv/homelab-foss \
  --branch=main \
  --private-key-file=/Users/ryanb/iCloud/keys/github/id_ed25519-github \
  --path=src/fluxcd/clusters/dt
```

# Upgrade Flux

Doc: 

``` bash
flux install --export > ./src/fluxcd/clusters/<name>/flux-system/gotk-components.yaml
```
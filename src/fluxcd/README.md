# Install Flux 

Doc: 

``` bash
flux install --namespace=flux-system

flux create source git homelab-foss \
  --url=https://git@github.com/ryanbtv/homelab-foss \
  --branch=main
```

# Upgrade Flux

Doc: 

``` bash
flux install --export > ./src/fluxcd/clusters/<name>/flux-system/gotk-components.yaml
```
# k8s-gitops


```bash

flux install --version=latest \
  --arch=amd64 \
  --cluster-domain=vagrant.local \
  --export > ./cluster/flux-system/gotk-components.yaml

kubectl create ns flux-system

kubectl apply -f cluster/flux-system/gotk-components.yaml
flux check

flux create source git flux-system \
  --url=ssh://git@github.com/pando85/k8s-gitops.git \
  --ssh-key-algorithm=ecdsa \
  --ssh-ecdsa-curve=p521 \
  --branch=test-env \
  --interval=1m

flux create kustomization flux-system \
  --source=flux-system \
  --path="./cluster" \
  --prune=true \
  --interval=10m


flux export source git flux-system \
  > ./cluster/flux-system/gotk-sync.yaml

flux export kustomization flux-system \
  >> ./cluster/flux-system/gotk-sync.yaml
```


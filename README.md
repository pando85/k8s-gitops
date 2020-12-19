# k8s-gitops


```bash
flux install --version=latest \
  --arch=amd64 \
  --export > ./cluster/flux-system/gotk-components.yaml

# Replace cluster.local with your cluster_domain in gotk-components

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

```


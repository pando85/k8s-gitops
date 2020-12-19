# k8s-gitops


```bash
flux install --version=latest \
  --arch=amd64 \
  --export > ./cluster/flux-system/gotk-components.yaml

kubectl create ns flux-system

kubectl apply -f cluster/flux-system/gotk-components.yaml
flux check

```


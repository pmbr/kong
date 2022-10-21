# Kong API Gateway Cookbook

Instructions and recipes for setting up Kong API Gateway.

## Kong as ingress controller

Using Kong as ingress controller works basically as a proxy in front of actual services routing requests to target.

## Deploying Kong proxy

```kubectl apply -f kong-ingress-controller.yaml```

(yaml source)[https://raw.githubusercontent.com/Kong/kubernetes-ingress-controller/v2.7.0/deploy/single/all-in-one-dbless.yaml] provided by Kong documentation refering to deploying an ingress controller to an (AKS)[https://docs.konghq.com/kubernetes-ingress-controller/2.7.x/deployment/aks/] cluster.

It worth saying that a change seemed to be required to correctly expose kong proxy service on AKS.

Original file was using annotations for AWS:

https://github.com/Kong/kubernetes-ingress-controller/blob/v2.7.0/deploy/single/all-in-one-dbless.yaml#L1516

New file is using annotations for AKS:

```service.beta.kubernetes.io/azure-load-balancer-internal: "true"```

### Configuring ingress rule

Refer to kong-proxy-ingress-foo-rule.yaml

## Reference links

(all-in-one-enterprise)[https://raw.githubusercontent.com/Kong/kubernetes-ingress-controller/v2.7.0/deploy/single/all-in-one-postgres-enterprise.yaml]

(AKS)[https://docs.konghq.com/kubernetes-ingress-controller/2.7.x/deployment/aks/]

(Getting started to ingress controller)[https://docs.konghq.com/kubernetes-ingress-controller/2.7.x/guides/getting-started/]

(Set up a Kong Gateway Runtime on Kubernetes)[https://docs.konghq.com/konnect/runtime-manager/runtime-instances/gateway-runtime-kubernetes/]

https://docs.konghq.com/kubernetes-ingress-controller/latest/references/annotations/#multiple-unrelated-controllers

https://github.com/Kong/charts/blob/main/charts/kong/README.md

## Ignore everything below this line

kubectl  --context art-nonprod-westus-1-linux1-aks

kubectl  --context art-nonprod-westus-1-linux1-aks -n kong apply -f kong-ingress-controller.yaml

kubectl  --context art-nonprod-westus-1-linux1-aks -n int apply -f kong-ingress-art-product-service.yaml
kubectl  --context art-nonprod-westus-1-linux1-aks -n int apply -f kong-ingress-art-search-service.yaml
kubectl  --context art-nonprod-westus-1-linux1-aks -n int apply -f kong-ingress-art-seo-service.yaml

kubectl  --context art-nonprod-westus-1-linux1-aks -n npp5 apply -f kong-ingress-apc-product-service.yaml
kubectl  --context art-nonprod-westus-1-linux1-aks -n npp5 apply -f kong-ingress-apc-search-service.yaml



/Users/p0b05qr/repos/art/kube-charts/charts
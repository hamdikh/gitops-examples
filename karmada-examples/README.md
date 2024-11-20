# GitOps with Karmada

Follow these steps to deploy Karmada using Helm.

## Add Karmada Helm Repository

First, add the Karmada Helm repository and update it:

```bash
helm repo add karmada-charts https://raw.githubusercontent.com/karmada-io/karmada/master/charts
helm repo update
```

## Install Karmada

Install Karmada in the `karmada-system` namespace:

```bash
helm install karmada -n karmada-system --create-namespace --dependency-update karmada-charts/karmada
```

## Export Karmada KubeConfig

Export the Karmada KubeConfig to your local directory:

```bash
kubectl get secret -n karmada-system karmada-kubeconfig -o jsonpath={.data.kubeconfig} | base64 -d > ~/.kube/karmada-apiserver.config
```

> **Note:** You may want to use `localhost` if you're planning on port-forwarding the Karmada service.

## Create Multiple Kind Clusters

Create multiple Kind clusters to use with Karmada:

```bash
kind create cluster --name hkh-gitops-demo-1
kind create cluster --name hkh-gitops-demo-2
kind create cluster --name hkh-gitops-demo-3
kind create cluster --name hkh-gitops-demo-4
```

## Join Clusters (Push Mode)

Join clusters to Karmada using push mode:

```bash
karmadactl join kind-hkh-gitops-demo-2 --kubeconfig ~/.kube/karmada-apiserver.config --karmada-context karmada-apiserver --cluster-kubeconfig ~/.kube/config --cluster-context kind-hkh-gitops-demo-2

karmadactl join kind-hkh-gitops-demo-3 --kubeconfig ~/.kube/karmada-apiserver.config --karmada-context karmada-apiserver --cluster-kubeconfig ~/.kube/config --cluster-context kind-hkh-gitops-demo-3
```

<!--
## Join Clusters (Pull Mode)

Generate a token and register clusters using pull mode:

```bash
karmadactl token create --print-register-command --kubeconfig ~/.kube/karmada-apiserver.config

karmadactl register localhost:5443 --cluster-name kind-hkh-gitops-demo-4 --token <your-token> --discovery-token-ca-cert-hash <your-hash>
```
-->
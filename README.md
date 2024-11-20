# gitops-examples

## Installing and Creating a Kind Cluster

To install Kind, follow these steps:

1. Install Kind by running the following command:
    ```sh
    curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.25.0/kind-linux-amd64
    chmod +x ./kind
    mv ./kind /usr/local/bin/kind
    ```

2. Create a new Kind cluster:
    ```sh
    kind create cluster --name gitops-demo
    ```

## Introduction to GitOps

GitOps is a way of implementing Continuous Deployment for cloud-native applications. It uses Git as a single source of truth for declarative infrastructure and applications. With GitOps, you can manage your infrastructure and application configurations using Git, allowing for version control, collaboration, and easy rollbacks.

## Examples with Flux and ArgoCD

In this repository, we will provide examples of how to implement GitOps using two popular tools: Flux and ArgoCD. These examples will demonstrate how to set up and manage your Kubernetes clusters and applications using GitOps principles.
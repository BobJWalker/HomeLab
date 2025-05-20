# Configuration

The docker image, manifest files, and variables will be provided to you.

## 1. Install K8s
Install **_ONE_** of the following on a VM or locally!

- [docker desktop](https://docs.docker.com/desktop/) - easiest and preferred
  - 🍎 If you are working on a Mac with an Apple chip—Docker Desktop is the easiest option:
    - Run [`softwareupdate --install-rosetta`](https://docs.docker.com/desktop/install/mac-install/#system-requirements)
    - Enable [Kubernetes](https://docs.docker.com/desktop/kubernetes/#install-and-turn-on-kubernetes)
    - Confirm `Use Virtualization framework` is enabled in Docker Desktop → General → Settings
- [rancher desktop](https://docs.rancherdesktop.io/getting-started/installation) -> please note you will not have to install docker for this to work.
- [minikube](https://minikube.sigs.k8s.io/docs/start/)

## 2. Install Octopus K8s Agent

Follow the instructions in [Octopus Deploy Docs](https://octopus.com/docs/kubernetes/targets/kubernetes-agent) to install the Kubernetes Agent.

## 3. Install Infrastructure

- Run `kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.5/deploy/static/provider/cloud/deploy.yaml`
- Run `helm repo add secrets-store-csi-driver https://kubernetes-sigs.github.io/secrets-store-csi-driver/charts`
- Run `helm repo update`
- Run `helm install csi-secrets-store secrets-store-csi-driver/secrets-store-csi-driver --namespace kube-system --set syncSecret.enabled=true`
- Run `kubectl apply -f https://raw.githubusercontent.com/Azure/secrets-store-csi-driver-provider-azure/refs/heads/master/deployment/provider-azure-installer.yaml`
- Run `kubectl apply -f k8s/azure-principle.yaml`

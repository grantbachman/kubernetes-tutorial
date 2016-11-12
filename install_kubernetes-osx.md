# Install and test kubernetes on OSX

Kubernetes handles the orchestration of docker containers in a cloud environment.

## Test Locally
Testing locally is important, because only savages test in the cloud. Testing locally requires Kubectl and Minikube.

  1. [Install Kubectl](http://kubernetes.io/docs/getting-started-guides/minikube/#install-kubectl): `curl -Lo kubectl http://storage.googleapis.com/kubernetes-release/release/v1.3.0/bin/darwin/amd64/kubectl && chmod +x kubectl && sudo mv kubectl /usr/local/bin/`
    * Kubectl comes bundled when you pick/download a kubernetes cloud provider implementation, but since we're only concerned with local right now, we
can download it straight.
  2. [Install Minikube](https://github.com/kubernetes/minikube/releases): `curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.12.2/minikube-darwin-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/`
    * Minikube is a tool that makes it easy to deal with kubernetes locally.

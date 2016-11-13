# Install and test kubernetes on OSX

Kubernetes handles the orchestration of docker containers in a cloud environment.

## Running Locally
Running locally is important for getting configuration right before deploying a cluster. Running locally requires Kubectl and Minikube.

  1. [Install Kubectl](http://kubernetes.io/docs/getting-started-guides/minikube/#install-kubectl): `curl -Lo kubectl http://storage.googleapis.com/kubernetes-release/release/v1.3.0/bin/darwin/amd64/kubectl && chmod +x kubectl && sudo mv kubectl /usr/local/bin/`
    * Kubectl comes bundled when you pick/download a kubernetes cloud provider implementation, but since we're only concerned
    with local right now, wecan download it straight.
  2. [Install Minikube](https://github.com/kubernetes/minikube/releases): `curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.12.2/minikube-darwin-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/`
    * Minikube is a tool that makes it easy to deal with kubernetes locally. Trying to figure out IP addresses across containers/pods/nodes is hard enough without adding the VM necessary to run it locally.

# Test Locally
[Reference](https://github.com/kubernetes/minikube/blob/v0.12.2/README.md)

1. Start a cluster locally: `minikube start`
2. Push your image to [a docker image repository](https://hub.docker.com/) so that Kubernetes can find it.
  1. `docker tag api grantbachman/api`
  * `docker push grantbachman/api`
  * Another option is to run `eval $(minikube docker-env)`, which binds the docker daemon running on your machine to the docker daemon running inside the minikube VM. **When doing this
  you must build images with a tag like *api:v1* (not *api*)**. You can then rebuild the image and it'll be available for reference in Step 3. [Reference](https://www.brandpending.com/2016/09/20/using-minikube-as-a-local-kubernetes-test-and-development-environment-on-macos/).
3. Deploy this container as a pod: `kubectl run api --image=grantbachman/api --port=5000`
  * `kubectl run api` creates a pod called `api`
  * `--image=grantbachman/api` uses the image hosted at Docker Hub as the thing that should run inside the pod. You can specify any docker repository here.
  * `--port=5000` tells docker to expose port 5000 on the container so our cluster can access it.
4. Expose this pod so it is accessible outside the cluster: `kubectl expose deployment api --port=80 --target-port=5000 --type=LoadBalancer`
  * `kubectl expose deployment api` tells Kubernetes to create a service that points to the `api` pod.
  * `--port=80 --targe-port=5000` tells Kubernetes that the service is accessible via port 80, and should point to the pod's port 5000.
  * `--type=LoadBalancer` tells Kubernetes to throw a loadbalancer in front of the service. We could specify `--type=NodePort` instead if we want to expose it without a loadbalancer.
5. Test that you can access the API: `minikube service api`
  * This will open the service in your default browser.
  * This is helpful to figure out how we know the IP of this service: `kubectl describe service api`
6. Destroy the service/deployment: `kubectl delete service,deployment api`
7. Destroy the cluster: `minikube delete`

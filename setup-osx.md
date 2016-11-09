# How to bring up a Flask project using Docker/Kubernetes

## Set up a Kubernetes cluster on AWS
1. `cd /path/to/project`
2. `export KUBERNETES_PROVIDER=aws; curl -sS https://get.k8s.io | bash`
  * This command does it all in one script, including bringing up master/minion EC2 instances, creating a VPC, configuring routes, etc. 

## Tear down Kubernetes cluster on AWS
1. `cd /path/to/project/kubernetes`
2. `cluster/kube-down.sh`

## References
 * http://kubernetes.io/docs/getting-started-guides/aws/

# Set up Kubernetes on OSX
1. `cd /path/to/project`
2. Download Kubernetes scripts and bring up an AWS cluster: `export KUBERNETES_PROVIDER=aws; curl -sS https://get.k8s.io | bash`
3. Make `kubectl` script available: `export PATH=/path/to/project/kubernetes/platforms/darwin/amd64:$PATH`

## References
 * http://kubernetes.io/docs/getting-started-guides/aws/

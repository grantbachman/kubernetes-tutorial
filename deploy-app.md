# Deploy an app on Kubernetes cluster
1. `cd /path/to/project`
2. Make kubectl script available in the shell:
`export PATH=/path/to/project/kubernetes/platforms/darwin/amd64:$PATH`
3. `kubectl run api --image=xxxxx.dkr.ecr.us-east-1.amazonaws.com/repo-name --port=5000`
4. Expose api via an ELB (Elastic LoadBalancer): `kubectl expose deployment api --port=80 --target-port=5000 --type=LoadBalancer`

## References
 * http://kubernetes.io/docs/user-guide/simple-nginx/

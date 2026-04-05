### startup

// enable autocomplete for zsh
echo 'source <(kubectl completion zsh)' >> ~/.zshrc
echo 'alias k=kubectl' >> ~/.zshrc
echo 'compdef \_kubectl k' >> ~/.zshrc

### fundamental commands

// check kube config
k config view

// change context
k config use-context <context-name>

// set default namespace for current conext
k config set-context --current --namespace=default

// get all pods in current namespace
k get pods -o wide
// get all pods from all namespace
k get pods -A -o wide
(\* add -o wide to watch ip/node)

// get detail of a pods
k descirbe pod <pod-name>

// check nodes status
k get nodes

// lists all recent activities and errors(events)
k get events --sort-by=.metadata.creationTimestamp

// trick use jsonpath to get only info wanted
<k get pods -A> -o jsonpath='{.items[*].metadata.name}'
//(\* `-o json` could be use to check json struct)

### resource creation

// create a resource definition YAML

```bash
cat << EOF > my-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
EOF
```

// create resource by apply YAML file
`k apply -f my-pod.yaml`

// use impertive to create resource (command under create a deployment)
`k create deployment my-dep --image=nginx`

// to delete a resource
`k delete <resource-type> <resource-name>`
sample: `k delete deployment my-dep`

### Other fundamental commands

// exec inside pod
`k exec -it <pod-name> -- /bin/sh`

// check logs of a pod
`k logs <pod-name>`

// port-forward
`k port-forward pod/nginx 8080:80`

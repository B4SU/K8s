

|                               |                                                         |
|-------------------------------|---------------------------------------------------------|
|kubectl get nodes              | List nodes                                              |
|kubectl get pods               | List pods                                               |
|kubectl get pods -o wide       | List all pods with more information (such as node name) |
|kubectl describe pod n1        | Describe resource                                       |


```sh
# Create basic pod using image
kubectl run n1 --image nginx
```

```sh
# Create pod from yaml file
kubectl create -f pod-defination.yml

# See details about configured pod
kubectl describe pod mypod

```

```sh
# View manifest file of an existing image
kubectl run pod2 --image nginx --dry-run=client -o yaml
```

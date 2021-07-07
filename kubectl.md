# kubectl

This is my cheatsheet for anything related to `kubectl`

* How to get api versions present in a kubernetes api server?

```bash
$ kubectl api-versions
```

* How to get api resources present in a kubernetes api server?

```bash
$ kubectl api-resources
```

* How to find all the fields present in a resource? To write a yaml file for
the resource

You can use kubectl explain

```bash
$ kubectl explain pod
$ kubectl explain pod.spec
$ kubectl explain pod.spec.containers
# containers is an array field, for sub fields in containers, you can just do -
$ kubectl explain pod.spec.containers.volumeMounts
```

* How to get a resource? Pods, Nodes, and more, and then Custom Resources

```bash
$ kubectl get pods
$ kubectl get nodes
# custom resource definitions
$ kubectl get customresourcedefinitions
# an example custom resource called application / applications
$ kubectl get applications
```

* How to know if I have the permission to do something or not, without doing it?

For example - can you delete a pod? create a pod?

```bash
$ kubectl auth can-i delete pod
$ kubectl auth can-i create pod
```

* How to change the output format of the output?

Usually most commands and sub commands have a `--output` / `-o` flag. Use `--help` / `-h` to know if the output flag exists and what are the valid values for it

```bash
$ kubectl get pod --output yaml
$ kubectl get pod --output json
$ kubectl get pod -o json
```

* How to do a rollback for some resources? Like deployments, daemonsets, statefulsets

```bash
$ kubectl rollout undo deployment/coredns --namespace kube-system
$ kubectl rollout undo daemonset/some-app --to-revision=3
$ kubectl rollout undo statefulset/some-other-app
```

* How to change the editor to edit resources?

```bash
$ EDITOR="code -w" kubectl edit deployment/coredns -n kube-system
```

The above assumes Visual Studio Code as the editor. The `-w` flag is for waiting for the user's input to edit the deployment and save it and close it. Only after closing, the command will continue running and then come to completion. Till the time the user closes the editor, the command will be paused and blocking and will keep waiting for the user to close the editor

* How to find the IP address of the pods?

```bash
# shows IP in one of the tabular columns. It has pod names and pod IPs
$ kubectl get pod -o wide
# IP field
$ kubectl describe pod demo-app
# using jq get all pod IPs. Just IPs, no pod names
$ kubectl get pod -o json | jq -r '.items[].status.podIP'
# both pod name and pod IP
$ kubectl get pod -A -o json | jq -r '.items[] | { name: .metadata.name, ip: .status.podIP }'
# similar thing as above but without using jq and instead using jsonpath
# https://kubernetes.io/docs/reference/kubectl/jsonpath/
$ kubectl get pod -o jsonpath='{range .items[*]}{.status.podIP}{"\n"}{end}'
$ kubectl get pod -o jsonpath='{range .items[*]}{.metadata.name} : {.status.podIP}{"\n"}{end}'
```

* How to find the node in which a pod runs?

```bash
# shows node name in one of the tabular columns. It has pod names and node names
$ kubectl get pod -o wide
# Node field
$ kubectl describe pod demo-app
```

* How to find all the pods running in a node?

One can see the non-terminated (not terminated) pods using this -

```bash
# under "Non-terminated Pods" field
$ kubectl describe node worker-node-1
```

* How to find the number of disks attached to a node?

* How to find the total number of disks that can be attached to a node?

* How to get the PVC size for all PVCs? How to apply filters in this?

* How to get the resources and requests for all deployments? How to apply
filters in it?

* How to retrieve resources based on kubernetes labels?

* How to execute into a pod? execute into a kubernetes deployment?

* How to port forwward a pod? port forward a kubernetes service?

* How to show labels for all the resources you retrieve?

* How to order pods by the time it started at? With recent ones coming at the
bottom and the vice versa

* How to find the API calls made by kubectl to the Kubernetes API server?

Use higher number for the log verbosity in `kubectl`. For example use `-v 8` or more bigger numbers

```bash
$ kubectl describe node -v 8
```

* How to remove / delete all the users in the kube config?

```bash
$ kubectl config get-users | xargs -I {} kubectl config delete-user {}
```

* How to remove / delete all the clusters in the kube config?

```bash
$ kubectl config get-clusters | xargs -I {} kubectl config delete-cluster {}
```

* How to remove / delete all the contexts in the kube config?

```bash
$ kubectl config get-contexts -o name | xargs -I {} kubectl config delete-context {}
```

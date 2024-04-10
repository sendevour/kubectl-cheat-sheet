# kubectl-cheat-sheet
Cheat sheet for kubectl tool

## Short name for resources

$ kubectl api-resources

| Short name           | Full name                    |
| -------------------- | ---------------------------- |
|  csr                 |  certificatesigningrequests  |
|  cs                  |  componentstatuses           |
|  cm                  |  configmaps                  |
|  crd                 |  customresourcedefinitions   |
|  cj                  |  cronjobs                    |
|  ds                  |  daemonsets                  |
|  deploy              |  deployments                 |
|  ep                  |  endpoints                   |
|  ev                  |  events                      |
|  hpa                 |  horizontalpodautoscalers    |
|  ing                 |  ingresses                   |
|  limits              |  limitranges                 |
|  netpol              |  networkpolicies             |
|  ns                  |  namespaces                  |
|  no                  |  nodes                       |
|  pvc                 |  persistentvolumeclaims      |
|  pv                  |  persistentvolumes           |
|  po                  |  pods                        |
|  pdb                 |  poddisruptionbudgets        |
|  psp                 |  podsecuritypolicies         |
|  rs                  |  replicasets                 |
|  rc                  |  replicationcontrollers      |
|  quota               |  resourcequotas              |
|  sa                  |  serviceaccounts             |
|  svc                 |  services                    |
|  sts                 |  statefulsets                |
|  sc                  |  storageclasses              |


| Short name       | Full name                 |
| ---------------- | ------------------------- |
|  -n production   |  --namespace=production   |
|  -A              |  --all-namespaces=true    |

## Setting up autocomplete and alias in mac

Copy below lines in ~/.zshrc and reload the terminal.
```
autoload -Uz compinit
compinit
alias k=kubectl
source <(kubectl completion zsh)
```

## Install kubectl convert plugin
A plugin for Kubernetes command-line tool kubectl, which allows you to convert manifests between different API versions. This can be particularly helpful to migrate manifests to a non-deprecated api version with newer Kubernetes release. For more info, visit migrate to non deprecated apis.
Refer, https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/#install-kubectl-convert-plugin

Viewing Resource Information

Nodes
```
$ kubectl get no
$ kubectl get no -o wide
$ kubectl describe no
$ kubectl get no -o yaml
$ kubectl get node --select or =[ label _name]
$ kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="ExternalIP")].address}'
$ kubectl top node [node_name]
```

Delete StatefulSet only (not pods)
```
kubectl delete statefulset/[stateful_set_name] --cascade=false
```

Pods
```
$ kubectl get po
$ kubectl get po -o wide
$ kubectl describe po
$ kubectl get po --show-labels
$ kubectl get po -l app=nginx
$ kubectl get po -o yaml
$ kubect l get pod [ pod_name] -o yaml --export
$ kubect l get pod [pod_name] -o yaml --export > nameoffile.yaml
$ kubectl get pods --field-selector status.phase=Running
```
Namespaces
```
$ kubectl get ns
$ kubectl get ns -o yaml
$ kubectl describe ns
```
Deployments
```
$ kubectl get deploy
$ kubectl describe deploy
$ kubectl get deploy -o wide
$ kubectl get deploy -o yaml
```
Services
```
$ kubectl get svc
$ kubectl describe svc
$ kubectl get svc -o wide
$ kubectl get svc -o yaml
$ kubectl get svc --show-labels
```
DaemonSets
```
$ kubectl get ds
$ kubectl get ds --all-namespaces
$ kubectl describe ds [daemonset _name] -n [namespace_name]
$ kubectl get ds [ds_name] -n [ns_name] -o yaml
```
Events
```
$ kubectl get events
$ kubectl get events -n kube-system
$ kubectl get events -w
```
Logs
```
$ kubectl logs [pod_name]
$ kubectl logs --since=1h [pod_name]
$ kubectl logs --tail =20 [pod_name]
$ kubectl logs -f -c [container_name] [pod_name]
$ kubectl logs [pod_name] > pod.log
```
Service Accounts
```
$ kubectl get sa
$ kubectl get sa -o yaml
$ kubectl get serviceaccounts default -o yaml > ./sa.yaml
$ kubectl replace serviceaccount default -f. /sa.yaml
```
ReplicaSets
```
$ kubectl get rs
$ kubectl describe rs
$ kubectl get rs -o wide
$ kubectl get rs -o yaml
```
Roles
```
$ kubectl get roles --all-namespaces
$ kubectl get roles --all-namespaces -o yaml
```
Secrets
```
$ kubectl get secrets
$ kubectl get secrets --all-namespaces
$ kubectl get secrets -o yaml
```
ConfigMaps
```
$ kubectl get cm
$ kubectl get cm --all-namespaces
$ kubectl get cm --all-namespaces -o yaml
```
Ingress
```
$ kubectl get ing
$ kubectl get ing --all-namespaces
```
PersistentVolume
```
$ kubectl get pv
$ kubectl describe pv
```
PersistentVolumeClaim
```
$ kubectl get pvc
$ kubectl describe pvc
```
StorageClass
```
$ kubectl get sc
$ kubectl get sc -o yaml
```
MultipleResources
```
$ kubectl get svc, po
$ kubectl get deploy, no
$ kubectl get all
$ kubectl get all --all-namespaces
```
Changing Resource Attributes

Taint
```
$ kubectl taint [node_name] [taint _name]
```
Labels
```
$ kubectl label [node_name] disktype=ssd
$ kubrectl label [pod_name] env=prod
```
Cordon/Uncordon
```
$ kubectl cordon [node_name]
$ kubectl uncordon [node_name]
```
Drain
```
$ kubectl drain [node_name]
```
Nodes/Pods
```
$ kubectl delete node [node_name]
$ kubectl delete pod [pod_name]
$ kubectl edit node [node_name]
$ kubectl edit pod [pod_name]
```
Deployments/Namespaces
```
$ kubectl edit deploy [deploy_name]
$ kubectl delete deploy [deploy_name]
$ kubectl expose deploy [depl oy_name] --port=80 --type=NodePort
$ kubectl scale deploy [deploy_name] --replicas=5
$ kubectl delete ns
$ kubectl edit ns [ns_name]
```
Services
```
$ kubectl edit svc [svc_name]
$ kubectl delete svc [svc_name]
```
DaemonSets
```
$ kubectl edit ds [ds_name] -n kube-system
$ kubectl delete ds [ds_name]
```
ServiceAccounts
```
$ kubectl edit sa [sa_name]
$ kubectl delete sa [sa_name]
```
Annotate
```
$ kubectl annotate po [pod_name] [annotation]
$ kubectl annotate no [node_name]
```
Adding Resources

Creating a Pod
```
$ kubectl create -f [name_of _file]
$ kubectl apply -f [name_of _file]
$ kubectl run [pod_name] --image=ngi nx --restart=Never
$ kubectl run [ pod_name] --generator =run-pod/v1 --image=nginx
$ kubectl run [ pod_name] --image=nginx --restart=Never
```
Creating a Service
```
$ kubectl create svc nodeport [svc_name] --tcp=8080:80
```
Creating a Deployment
```
$ kubectl create -f [name_of _file]
$ kubectl apply -f [name_of _file]
$ kubectl create deploy [deploy_name] --image=nginx
```
Interactive Pod
```
$ kubectl run [pod_name] --image=busybox --rm -it --restart=Never -- sh
```
Output YAMLto aFile
```
$ kubectl create deploy [deploy_name] --image=ngi nx --dry-run -o yaml > deploy.yaml
$ kubectl get po [pod_name] -o yaml --export > pod. yaml
```
Getting Help
```
$ kubectl -h
$ kubectl create -h
$ kubectl run -h
$ kubectl explain deploy.spec
```
Requests

API Call
```
$ kubectl get --raw /apis/metrics.k8s.io/
```
Cluster Info
```
$ kubectl config
$ kubectl cluster -info
$ kubectl get componentstatuses
```


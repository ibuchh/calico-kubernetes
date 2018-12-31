# Instructions

## Install Claico
```
kubectl apply -f calico.yaml
```
## Create Resources
```
kubectl apply -f namespace.yaml

kubectl apply -f management-ui.yaml
kubectl apply -f backend.yaml
kubectl apply -f frontend.yaml
kubectl apply -f client.yaml

$ kubectl get pods --all-namespaces


NAMESPACE       NAME                                                  READY   STATUS    RESTARTS   AGE
client          client-nkcfg                                          1/1     Running   0          24m
kube-system     aws-node-6kqmw                                        1/1     Running   0          50m
kube-system     aws-node-grstb                                        1/1     Running   1          50m
kube-system     aws-node-m7jg8                                        1/1     Running   1          50m
kube-system     calico-node-b5b7j                                     1/1     Running   0          28m
kube-system     calico-node-dw694                                     1/1     Running   0          28m
kube-system     calico-node-vtz9k                                     1/1     Running   0          28m
kube-system     calico-typha-75667d89cb-4q4zx                         1/1     Running   0          28m
kube-system     calico-typha-horizontal-autoscaler-78f747b679-kzzwq   1/1     Running   0          28m
kube-system     kube-dns-7cc87d595-bd9hq                              3/3     Running   0          1h
kube-system     kube-proxy-lp4vw                                      1/1     Running   0          50m
kube-system     kube-proxy-rfljb                                      1/1     Running   0          50m
kube-system     kube-proxy-wzlqg                                      1/1     Running   0          50m
management-ui   management-ui-wzvz4                                   1/1     Running   0          24m
stars           backend-tkjrx                                         1/1     Running   0          24m
stars           frontend-q4r84                                        1/1     Running   0          24m
```
### Summary

To summarize the different resources we created:

1. A namespace called stars
2. frontend and backend replication controllers and services within stars namespace
3. A namespace called management-ui
4. Replication controller and service management-ui for the user interface seen on the browser, in the management-ui namespace
5. A namespace called client
6. client replication controller and service in client namespace

## Access the management-ui service

```
kubectl get svc -o wide -n management-ui
```

## Apply Network Policies

```
kubectl apply -n stars -f default-deny.yaml

kubectl apply -n client -f default-deny.yaml
```
## Create Network Policies

```
kubectl apply -f allow-ui.yaml
kubectl apply -f allow-ui-client.yaml
```

Refresh the browser again and check the Network policies in place

## Allow DIrectional Traffic

```
kubectl apply -f backend-policy.yaml
kubectl apply -f frontend-policy.yaml
```

Upon refreshing your browser, you should be able to see the network policies in action.



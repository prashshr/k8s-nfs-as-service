# k8s-nfs-as-service

A Kubernetes sample project for deploying Statefulset with NFS.

## How to deploy:

```
kubectl create -f files/nfs-statefulset-test.yaml
CLUSTERIP=$(kubectl -n infrastructure get svc nfs-server | tail -1 | awk '{print $3}') ; echo $CLUSTERIP
sed -i 's/10.*$/'$CLUSTERIP'/' liveliness-pod-test.yaml ; grep -i server liveliness-pod-test.yaml
kubectl create -f files/liveliness-pod-test.yaml
```

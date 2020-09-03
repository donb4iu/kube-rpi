**[21:59:24]ubuntu@ubuntu:(192.168.2.50)~$ helm install kdash stable/kubernetes-dashboard**                          --set=image.repository=k8s.gcr.io/kubernetes-dashboard-arm64

```
WARNING: This chart is deprecated
NAME: kdash
LAST DEPLOYED: Wed Sep  2 21:59:40 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
*********************************************************************************
*** PLEASE BE PATIENT: kubernetes-dashboard may take a few minutes to install ***
*********************************************************************************

Get the Kubernetes Dashboard URL by running:
  export POD_NAME=$(kubectl get pods -n default -l "app=kubernetes-dashboard,release=kdash" -o jsonpath="{.items[0].metadata.name}")
  echo https://127.0.0.1:8443/
  kubectl -n default port-forward $POD_NAME 8443:8443
```
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

[23:57:14]ubuntu@ubuntu:(192.168.2.50)~$ kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')

```
Name:         admin-user-token-4bcsc
Namespace:    kubernetes-dashboard
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: ea3b4621-d269-4815-9cc6-f7613489d8ca

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1066 bytes
namespace:  20 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6Ikc5ZFNZNVJGTjlwazA3NmRCV3RrNFV6TkI1Z2VIdkNOTHBQTFhPVHd2ak0ifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLTRiY3NjIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiJlYTNiNDYyMS1kMjY5LTQ4MTUtOWNjNi1mNzYxMzQ4OWQ4Y2EiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZXJuZXRlcy1kYXNoYm9hcmQ6YWRtaW4tdXNlciJ9.x96dWJJplKlQUaH3lzvCvKnzAaOWfVOaK0mZqAseK5q-YfC0dAkF5XVDg8YfU7QBTAgiDezPlQK_NX0lEX4CxXf852IaWG_4WyxQtjAXlyu40IGsdzXn5o7AWCZvxPPEK4jJI08ptT2yQj9kYjJcx-AWwaB_9NvPpLMlrQXiPK_lKi3dLoKHSzr0jz15ki41ONB9d8gR8CyoLuf9D65aiQ4XQna1K8pFS2YVcP41BXixiiDub66XCbBgQ-Eq9fGGWuIwFs9RFUVG8kLa8PztAwaEXtMZmrQ2nUt2XQTVv7wNVMgNIJy5Az5vfGTUAiV5kX632o7QoLeAUEpRKi-c0Q
```
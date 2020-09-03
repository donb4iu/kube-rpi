# Accesssing kubernetes with ***Kubectl*** from workers

Make a note of two things: 
* first, the Kubernetes kubectl connection information has been written to /etc/kubernetes/admin.conf. 
    * This kubeconfig file can be copied to ~/.kube/config, either for root or a normal user on the master node or to a remote machine. 
    * This will allow you to control your cluster with the kubectl command.

* Second, the last line of the output starting with kubernetes join is a command you can run to join more nodes to the cluster.


# [Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)


## Deploying the Dashboard UI
   The Dashboard UI is not deployed by default. To deploy it, run the following command:
   
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
   
   
## Accessing the Dashboard UI
   To protect your cluster data, Dashboard deploys with a minimal RBAC configuration by default. Currently, Dashboard only supports logging in with a Bearer Token. To create a token for this demo, you can follow our guide on creating a [sample user](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md).
   
   Warning: The sample user created in the tutorial will have administrative privileges and is for educational purposes only.
   Command line proxy
   You can access Dashboard using the kubectl command-line tool by running the following command:
   
   kubectl proxy
   Kubectl will make Dashboard available at http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/.
   
   
## Sample User

### Creating a Service Account
* We are creating Service Account with name admin-user in namespace kubernetes-dashboard first.

```

cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
EOF
serviceaccount/admin-user created
```
### Creating a ClusterRoleBinding
* In most cases after provisioning cluster using kops, kubeadm or any other popular tool, the ClusterRole cluster-admin already exists in the cluster. We can use it and create only ClusterRoleBinding for our ServiceAccount. If it does not exist then you need to create this role first and grant required privileges manually.

```

cat <<EOF | kubectl apply -f -
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
EOF
clusterrolebinding.rbac.authorization.k8s.io/admin-user created
```

### Getting a Bearer Token
* Now we need to find token we can use to log in. Execute following command:
 
```
 
kubectl -n kubernetes-dashboard describe secret $(kubectl -n kubernetes-dashboard get secret | grep admin-user | awk '{print $1}')

Name:         admin-user-token-4bcsc
Namespace:    kubernetes-dashboard
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: ea3b4621-d269-4815-9cc6-f7613489d8ca

Type:  kubernetes.io/service-account-token

Data
====
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6Ikc5ZFNZNVJGTjlwazA3NmRCV3RrNFV6TkI1Z2VIdkNOTHBQTFhPVHd2ak0ifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLTRiY3NjIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiJlYTNiNDYyMS1kMjY5LTQ4MTUtOWNjNi1mNzYxMzQ4OWQ4Y2EiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZXJuZXRlcy1kYXNoYm9hcmQ6YWRtaW4tdXNlciJ9.x96dWJJplKlQUaH3lzvCvKnzAaOWfVOaK0mZqAseK5q-YfC0dAkF5XVDg8YfU7QBTAgiDezPlQK_NX0lEX4CxXf852IaWG_4WyxQtjAXlyu40IGsdzXn5o7AWCZvxPPEK4jJI08ptT2yQj9kYjJcx-AWwaB_9NvPpLMlrQXiPK_lKi3dLoKHSzr0jz15ki41ONB9d8gR8CyoLuf9D65aiQ4XQna1K8pFS2YVcP41BXixiiDub66XCbBgQ-Eq9fGGWuIwFs9RFUVG8kLa8PztAwaEXtMZmrQ2nUt2XQTVv7wNVMgNIJy5Az5vfGTUAiV5kX632o7QoLeAUEpRKi-c0Q
ca.crt:     1066 bytes
namespace:  20 bytes
```   

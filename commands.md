# [kubectl commands](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

## get nodes

**[06:20:45]ubuntu@ubuntu:(192.168.2.50)~$ kubectl get nodes -o wide**
```
NAME       STATUS   ROLES    AGE   VERSION   INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION     CONTAINER-RUNTIME
ubuntu     Ready    master   25h   v1.19.0   192.168.2.50   <none>        Ubuntu 20.04.1 LTS   5.4.0-1015-raspi   docker://19.3.8
ubuntu51   Ready    <none>   31m   v1.19.0   192.168.2.51   <none>        Ubuntu 20.04.1 LTS   5.4.0-1015-raspi   docker://19.3.8
ubuntu52   Ready    <none>   21s   v1.19.0   192.168.2.52   <none>        Ubuntu 20.04.1 LTS   5.4.0-1015-raspi   docker://19.3.8
```

## get pods

**[06:29:46]ubuntu@ubuntu:(192.168.2.50)~$ kubectl get pod --all-namespaces -o wide**
```
NAMESPACE     NAME                             READY   STATUS    RESTARTS   AGE     IP             NODE       NOMINATED NODE   READINESS GATES
kube-system   coredns-f9fd979d6-8hrz2          1/1     Running   0          25h     10.244.0.3     ubuntu     <none>           <none>
kube-system   coredns-f9fd979d6-hfn5l          1/1     Running   0          25h     10.244.0.2     ubuntu     <none>           <none>
kube-system   etcd-ubuntu                      1/1     Running   0          25h     192.168.2.50   ubuntu     <none>           <none>
kube-system   kube-apiserver-ubuntu            1/1     Running   0          25h     192.168.2.50   ubuntu     <none>           <none>
kube-system   kube-controller-manager-ubuntu   1/1     Running   0          25h     192.168.2.50   ubuntu     <none>           <none>
kube-system   kube-flannel-ds-arm64-4225s      1/1     Running   0          25h     192.168.2.50   ubuntu     <none>           <none>
kube-system   kube-flannel-ds-arm64-nrsfw      1/1     Running   0          37m     192.168.2.51   ubuntu51   <none>           <none>
kube-system   kube-flannel-ds-arm64-wlm6t      1/1     Running   0          6m21s   192.168.2.52   ubuntu52   <none>           <none>
kube-system   kube-proxy-5fsfj                 1/1     Running   0          6m21s   192.168.2.52   ubuntu52   <none>           <none>
kube-system   kube-proxy-8cbdj                 1/1     Running   0          37m     192.168.2.51   ubuntu51   <none>           <none>
kube-system   kube-proxy-ncdgg                 1/1     Running   0          25h     192.168.2.50   ubuntu     <none>           <none>
kube-system   kube-scheduler-ubuntu            1/1     Running   0          25h     192.168.2.50   ubuntu     <none>           <none>
```

## create namespace 
**[18:48:15]ubuntu@ubuntu:(192.168.2.50)~$ kubectl create namespace kube-verify**
```
namespace/kube-verify created
```

## get namespaces

**[23:07:46]ubuntu@ubuntu:(192.168.2.50)~$ kubectl get namespaces**
```
NAME              STATUS   AGE
default           Active   41h
kube-node-lease   Active   41h
kube-public       Active   41h
kube-system       Active   41h
kube-verify       Active   15s
```

## create deployment

**[23:08:01]ubuntu@ubuntu:(192.168.2.50)~$ cat <<EOF | kubectl create -f**- 
```
> apiVersion: apps/v1
> kind: Deployment
> metadata:
>   name: kube-verify
>   namespace: kube-verify
>   labels:
>     app: kube-verify
> spec:
>   replicas: 3
>   selector:
>     matchLabels:
>       app: kube-verify
>   template:
>     metadata:
>       labels:
>         app: kube-verify
>     spec:
>       containers:
>       - name: nginx
>         image: quay.io/clcollins/kube-verify:01
>         ports:
>         - containerPort: 8080
> EOF 

deployment.apps/kube-verify created

```
## get events

kubectl get events --all-namespaces  --sort-by='.metadata.creationTimestamp'

## get service IP

**[00:28:22]ubuntu@ubuntu:(192.168.2.50)~$ kubectl get -n kube-verify service/kube-verify**
```
NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
kube-verify   ClusterIP   10.105.119.235   <none>        80/TCP    19s
```
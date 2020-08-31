
**[06:07:01]ubuntu@ubuntu** :(192.168.2.52)~$ sudo usermod -aG docker ${USER}
**ubuntu@ubuntu** :/etc/docker$ systemctl status docker.service
```
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: failed (Result: exit-code) since Wed 2020-08-26 03:19:10 UTC; 11min ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
    Process: 2835 ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock (code=exited, status=1/FAILURE)
   Main PID: 2835 (code=exited, status=1/FAILURE)

Aug 26 03:19:10 ubuntu systemd[1]: docker.service: Scheduled restart job, restart counter is at 3.
Aug 26 03:19:10 ubuntu systemd[1]: Stopped Docker Application Container Engine.
Aug 26 03:19:10 ubuntu systemd[1]: docker.service: Start request repeated too quickly.
Aug 26 03:19:10 ubuntu systemd[1]: docker.service: Failed with result 'exit-code'.
Aug 26 03:19:10 ubuntu systemd[1]: Failed to start Docker Application Container Engine.
Aug 26 03:19:56 ubuntu systemd[1]: docker.service: Start request repeated too quickly.
Aug 26 03:19:56 ubuntu systemd[1]: docker.service: Failed with result 'exit-code'.
Aug 26 03:19:56 ubuntu systemd[1]: Failed to start Docker Application Container Engine.
```
**ubuntu@ubuntu**:/etc/docker$ systemctl start docker
```
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ===
Authentication is required to start 'docker.service'.
Authenticating as: Ubuntu (ubuntu)
Password:
==== AUTHENTICATION COMPLETE ===
```
**ubuntu@ubuntu**:/etc/docker$ systemctl status docker.service
```
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2020-08-26 03:31:30 UTC; 5s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 4262 (dockerd)
      Tasks: 14
     Memory: 45.8M
     CGroup: /system.slice/docker.service
             └─4262 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Aug 26 03:31:28 ubuntu dockerd[4262]: time="2020-08-26T03:31:28.861043527Z" level=warning msg="Your kernel does not support cgroup>
Aug 26 03:31:28 ubuntu dockerd[4262]: time="2020-08-26T03:31:28.861092710Z" level=warning msg="Your kernel does not support cgroup>
Aug 26 03:31:28 ubuntu dockerd[4262]: time="2020-08-26T03:31:28.861138820Z" level=warning msg="Your kernel does not support cgroup>
Aug 26 03:31:28 ubuntu dockerd[4262]: time="2020-08-26T03:31:28.862148301Z" level=info msg="Loading containers: start."
Aug 26 03:31:29 ubuntu dockerd[4262]: time="2020-08-26T03:31:29.500121894Z" level=info msg="Default bridge (docker0) is assigned w>
Aug 26 03:31:29 ubuntu dockerd[4262]: time="2020-08-26T03:31:29.856336276Z" level=info msg="Loading containers: done."
Aug 26 03:31:30 ubuntu dockerd[4262]: time="2020-08-26T03:31:30.270292359Z" level=info msg="Docker daemon" commit=afacb8b7f0 graph>
Aug 26 03:31:30 ubuntu dockerd[4262]: time="2020-08-26T03:31:30.272861340Z" level=info msg="Daemon has completed initialization"
Aug 26 03:31:30 ubuntu systemd[1]: Started Docker Application Container Engine.
Aug 26 03:31:30 ubuntu dockerd[4262]: time="2020-08-26T03:31:30.412318850Z" level=info msg="API listen on /run/docker.sock"
...skipping...
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2020-08-26 03:31:30 UTC; 5s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 4262 (dockerd)
      Tasks: 14
     Memory: 45.8M
     CGroup: /system.slice/docker.service
             └─4262 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Aug 26 03:31:28 ubuntu dockerd[4262]: time="2020-08-26T03:31:28.861043527Z" level=warning msg="Your kernel does not support cgroup>
Aug 26 03:31:28 ubuntu dockerd[4262]: time="2020-08-26T03:31:28.861092710Z" level=warning msg="Your kernel does not support cgroup>
Aug 26 03:31:28 ubuntu dockerd[4262]: time="2020-08-26T03:31:28.861138820Z" level=warning msg="Your kernel does not support cgroup>
Aug 26 03:31:28 ubuntu dockerd[4262]: time="2020-08-26T03:31:28.862148301Z" level=info msg="Loading containers: start."
Aug 26 03:31:29 ubuntu dockerd[4262]: time="2020-08-26T03:31:29.500121894Z" level=info msg="Default bridge (docker0) is assigned w>
Aug 26 03:31:29 ubuntu dockerd[4262]: time="2020-08-26T03:31:29.856336276Z" level=info msg="Loading containers: done."
Aug 26 03:31:30 ubuntu dockerd[4262]: time="2020-08-26T03:31:30.270292359Z" level=info msg="Docker daemon" commit=afacb8b7f0 graph>
Aug 26 03:31:30 ubuntu dockerd[4262]: time="2020-08-26T03:31:30.272861340Z" level=info msg="Daemon has completed initialization"
Aug 26 03:31:30 ubuntu systemd[1]: Started Docker Application Container Engine.
Aug 26 03:31:30 ubuntu dockerd[4262]: time="2020-08-26T03:31:30.412318850Z" level=info msg="API listen on /run/docker.sock"
```
**ubuntu@ubuntu**:/etc/docker$ docker run hello-world
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
256ab8fe8778: Pull complete
Digest: sha256:7f0a9f93b4aa3022c3a4c147a449bf11e0941a1fd0bf4a8e6c9408b2600777c5
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
**ubuntu@ubuntu**:/etc/docker$ sudo kubeadm init --token=${TOKEN} --kubernetes-version=v1.18.2 --pod-network-cidr=10.244.0.0/16
```
W0826 03:32:37.899317    4626 configset.go:202] WARNING: kubeadm cannot validate component configs for API groups [kubelet.config.k8s.io kubeproxy.config.k8s.io]
[init] Using Kubernetes version: v1.18.2
[preflight] Running pre-flight checks
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
did you l[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Starting the kubelet
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [ubuntu kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 192.168.2.50]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [ubuntu localhost] and IPs [192.168.2.50 127.0.0.1 ::1]
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [ubuntu localhost] and IPs [192.168.2.50 127.0.0.1 ::1]
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
W0826 03:35:29.384886    4626 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[control-plane] Creating static Pod manifest for "kube-scheduler"
W0826 03:35:29.389864    4626 manifests.go:225] the default kube-apiserver authorization-mode is "Node,RBAC"; using "Node,RBAC"
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests". This can take up to 4m0s
[apiclient] All control plane components are healthy after 35.070504 seconds
[upload-config] Storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config-1.18" in namespace kube-system with the configuration for the kubelets in the cluster
[upload-certs] Skipping phase. Please see --upload-certs
[mark-control-plane] Marking the node ubuntu as control-plane by adding the label "node-role.kubernetes.io/master=''"
[mark-control-plane] Marking the node ubuntu as control-plane by adding the taints [node-role.kubernetes.io/master:NoSchedule]
[bootstrap-token] Using token: jno24i.oyccq0fkdc1mkwxl
[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to get nodes
[bootstrap-token] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstrap-token] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstrap-token] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstrap-token] Creating the "cluster-info" ConfigMap in the "kube-public" namespace
[kubelet-finalize] Updating "/etc/kubernetes/kubelet.conf" to point to a rotatable kubelet client certificate and key
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.2.50:6443 --token jno24i.oyccq0fkdc1mkwxl \
    --discovery-token-ca-cert-hash sha256:9a61388bb5000eb78aca3339ebbc97faf951a97415cf74d2c4fa88e4a635ea6f
```
**ubuntu@ubuntu**:/etc/docker$ mkdir -p $HOME/.kube
**ubuntu@ubuntu**:/etc/docker$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
**ubuntu@ubuntu**:/etc/docker$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
**ubuntu@ubuntu**:/etc/docker$ kubectl get nodes
```
NAME     STATUS     ROLES    AGE     VERSION
ubuntu   NotReady   master   2m26s   v1.18.8
```
**ubuntu@ubuntu**:/etc/docker$ kubectl describe node ubuntu
```
Name:               ubuntu
Roles:              master
Labels:             beta.kubernetes.io/arch=arm64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=arm64
                    kubernetes.io/hostname=ubuntu
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Wed, 26 Aug 2020 03:36:04 +0000
Taints:             node-role.kubernetes.io/master:NoSchedule
                    node.kubernetes.io/not-ready:NoSchedule
Unschedulable:      false
Lease:
  HolderIdentity:  ubuntu
  AcquireTime:     <unset>
  RenewTime:       Wed, 26 Aug 2020 03:44:17 +0000
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Wed, 26 Aug 2020 03:41:30 +0000   Wed, 26 Aug 2020 03:35:54 +0000   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Wed, 26 Aug 2020 03:41:30 +0000   Wed, 26 Aug 2020 03:35:54 +0000   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Wed, 26 Aug 2020 03:41:30 +0000   Wed, 26 Aug 2020 03:35:54 +0000   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            False   Wed, 26 Aug 2020 03:41:30 +0000   Wed, 26 Aug 2020 03:35:54 +0000   KubeletNotReady              runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:docker: network plugin is not ready: cni config uninitialized
Addresses:
  InternalIP:  192.168.2.50
  Hostname:    ubuntu
Capacity:
  cpu:                4
  ephemeral-storage:  30368864Ki
  memory:             7998780Ki
  pods:               110
Allocatable:
  cpu:                4
  ephemeral-storage:  27987945017
  memory:             7896380Ki
  pods:               110
System Info:
  Machine ID:                 2d267d34a5104e34b6f4904f651b8cc3
  System UUID:                2d267d34a5104e34b6f4904f651b8cc3
  Boot ID:                    e401a2b9-312a-47e9-a3fc-90ec01ffc7b2
  Kernel Version:             5.4.0-1015-raspi
  OS Image:                   Ubuntu 20.04.1 LTS
  Operating System:           linux
  Architecture:               arm64
  Container Runtime Version:  docker://19.3.8
  Kubelet Version:            v1.18.8
  Kube-Proxy Version:         v1.18.8
PodCIDR:                      10.244.0.0/24
PodCIDRs:                     10.244.0.0/24
Non-terminated Pods:          (5 in total)
  Namespace                   Name                              CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
  ---------                   ----                              ------------  ----------  ---------------  -------------  ---
  kube-system                 etcd-ubuntu                       0 (0%)        0 (0%)      0 (0%)           0 (0%)         8m
  kube-system                 kube-apiserver-ubuntu             250m (6%)     0 (0%)      0 (0%)           0 (0%)         8m
  kube-system                 kube-controller-manager-ubuntu    200m (5%)     0 (0%)      0 (0%)           0 (0%)         8m
  kube-system                 kube-proxy-db2mg                  0 (0%)        0 (0%)      0 (0%)           0 (0%)         7m54s
  kube-system                 kube-scheduler-ubuntu             100m (2%)     0 (0%)      0 (0%)           0 (0%)         8m
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                550m (13%)  0 (0%)
  memory             0 (0%)      0 (0%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:
  Type    Reason                   Age                    From                Message
  ----    ------                   ----                   ----                -------
  Normal  NodeHasSufficientMemory  8m30s (x8 over 8m31s)  kubelet, ubuntu     Node ubuntu status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    8m30s (x8 over 8m31s)  kubelet, ubuntu     Node ubuntu status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     8m30s (x7 over 8m31s)  kubelet, ubuntu     Node ubuntu status is now: NodeHasSufficientPID
  Normal  Starting                 8m2s                   kubelet, ubuntu     Starting kubelet.
  Normal  NodeHasSufficientMemory  8m1s                   kubelet, ubuntu     Node ubuntu status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    8m1s                   kubelet, ubuntu     Node ubuntu status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     8m1s                   kubelet, ubuntu     Node ubuntu status is now: NodeHasSufficientPID
  Normal  NodeAllocatableEnforced  8m                     kubelet, ubuntu     Updated Node Allocatable limit across pods
  Normal  Starting                 7m52s                  kube-proxy, ubuntu  Starting kube-proxy.
```
**ubuntu@ubuntu**:/etc/docker$ kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```
podsecuritypolicy.policy/psp.flannel.unprivileged created
clusterrole.rbac.authorization.k8s.io/flannel created
clusterrolebinding.rbac.authorization.k8s.io/flannel created
serviceaccount/flannel created
configmap/kube-flannel-cfg created
daemonset.apps/kube-flannel-ds-amd64 created
daemonset.apps/kube-flannel-ds-arm64 created
daemonset.apps/kube-flannel-ds-arm created
daemonset.apps/kube-flannel-ds-ppc64le created
daemonset.apps/kube-flannel-ds-s390x created
```

**ubuntu@ubuntu**:/etc/docker$ kubectl get nodes
```
NAME     STATUS   ROLES    AGE   VERSION
ubuntu   Ready    master   11m   v1.18.8
```
**ubuntu@ubuntu**:/etc/docker$ kubectl describe node ubuntu
```
Name:               ubuntu
Roles:              master
Labels:             beta.kubernetes.io/arch=arm64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=arm64
                    kubernetes.io/hostname=ubuntu
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=
Annotations:        flannel.alpha.coreos.com/backend-data: {"VtepMAC":"62:21:9e:30:b0:3a"}
                    flannel.alpha.coreos.com/backend-type: vxlan
                    flannel.alpha.coreos.com/kube-subnet-manager: true
                    flannel.alpha.coreos.com/public-ip: 192.168.2.50
                    kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Wed, 26 Aug 2020 03:36:04 +0000
Taints:             node-role.kubernetes.io/master:NoSchedule
Unschedulable:      false
Lease:
  HolderIdentity:  ubuntu
  AcquireTime:     <unset>
  RenewTime:       Wed, 26 Aug 2020 03:47:37 +0000
Conditions:
  Type                 Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----                 ------  -----------------                 ------------------                ------                       -------
  NetworkUnavailable   False   Wed, 26 Aug 2020 03:47:24 +0000   Wed, 26 Aug 2020 03:47:24 +0000   FlannelIsUp                  Flannel is running on this node
  MemoryPressure       False   Wed, 26 Aug 2020 03:47:24 +0000   Wed, 26 Aug 2020 03:35:54 +0000   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure         False   Wed, 26 Aug 2020 03:47:24 +0000   Wed, 26 Aug 2020 03:35:54 +0000   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure          False   Wed, 26 Aug 2020 03:47:24 +0000   Wed, 26 Aug 2020 03:35:54 +0000   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready                True    Wed, 26 Aug 2020 03:47:24 +0000   Wed, 26 Aug 2020 03:47:24 +0000   KubeletReady                 kubelet is posting ready status. AppArmor enabled
Addresses:
  InternalIP:  192.168.2.50
  Hostname:    ubuntu
Capacity:
  cpu:                4
  ephemeral-storage:  30368864Ki
  memory:             7998780Ki
  pods:               110
Allocatable:
  cpu:                4
  ephemeral-storage:  27987945017
  memory:             7896380Ki
  pods:               110
System Info:
  Machine ID:                 2d267d34a5104e34b6f4904f651b8cc3
  System UUID:                2d267d34a5104e34b6f4904f651b8cc3
  Boot ID:                    e401a2b9-312a-47e9-a3fc-90ec01ffc7b2
  Kernel Version:             5.4.0-1015-raspi
  OS Image:                   Ubuntu 20.04.1 LTS
  Operating System:           linux
  Architecture:               arm64
  Container Runtime Version:  docker://19.3.8
  Kubelet Version:            v1.18.8
  Kube-Proxy Version:         v1.18.8
PodCIDR:                      10.244.0.0/24
PodCIDRs:                     10.244.0.0/24
Non-terminated Pods:          (8 in total)
  Namespace                   Name                              CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
  ---------                   ----                              ------------  ----------  ---------------  -------------  ---
  kube-system                 coredns-66bff467f8-tjthm          100m (2%)     0 (0%)      70Mi (0%)        170Mi (2%)     11m
  kube-system                 coredns-66bff467f8-w4m94          100m (2%)     0 (0%)      70Mi (0%)        170Mi (2%)     11m
  kube-system                 etcd-ubuntu                       0 (0%)        0 (0%)      0 (0%)           0 (0%)         11m
  kube-system                 kube-apiserver-ubuntu             250m (6%)     0 (0%)      0 (0%)           0 (0%)         11m
  kube-system                 kube-controller-manager-ubuntu    200m (5%)     0 (0%)      0 (0%)           0 (0%)         11m
  kube-system                 kube-flannel-ds-arm64-bcxg8       100m (2%)     100m (2%)   50Mi (0%)        50Mi (0%)      39s
  kube-system                 kube-proxy-db2mg                  0 (0%)        0 (0%)      0 (0%)           0 (0%)         11m
  kube-system                 kube-scheduler-ubuntu             100m (2%)     0 (0%)      0 (0%)           0 (0%)         11m
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                850m (21%)  100m (2%)
  memory             190Mi (2%)  390Mi (5%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:
  Type    Reason                   Age                From                Message
  ----    ------                   ----               ----                -------
  Normal  NodeHasSufficientMemory  11m (x8 over 11m)  kubelet, ubuntu     Node ubuntu status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    11m (x8 over 11m)  kubelet, ubuntu     Node ubuntu status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     11m (x7 over 11m)  kubelet, ubuntu     Node ubuntu status is now: NodeHasSufficientPID
  Normal  Starting                 11m                kubelet, ubuntu     Starting kubelet.
  Normal  NodeHasSufficientMemory  11m                kubelet, ubuntu     Node ubuntu status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    11m                kubelet, ubuntu     Node ubuntu status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     11m                kubelet, ubuntu     Node ubuntu status is now: NodeHasSufficientPID
  Normal  NodeAllocatableEnforced  11m                kubelet, ubuntu     Updated Node Allocatable limit across pods
  Normal  Starting                 11m                kube-proxy, ubuntu  Starting kube-proxy.
  Normal  NodeReady                14s                kubelet, ubuntu     Node ubuntu status is now: NodeReady
```
**ubuntu@ubuntu**:/etc/docker$ kubectl get pod --all-namespaces -o wide
```
NAMESPACE     NAME                             READY   STATUS    RESTARTS   AGE   IP             NODE     NOMINATED NODE   READINESS GATES
kube-system   coredns-66bff467f8-tjthm         1/1     Running   0          11h   10.244.0.2     ubuntu   <none>           <none>
kube-system   coredns-66bff467f8-w4m94         1/1     Running   0          11h   10.244.0.3     ubuntu   <none>           <none>
kube-system   etcd-ubuntu                      1/1     Running   0          11h   192.168.2.50   ubuntu   <none>           <none>
kube-system   kube-apiserver-ubuntu            1/1     Running   0          11h   192.168.2.50   ubuntu   <none>           <none>
kube-system   kube-controller-manager-ubuntu   1/1     Running   0          11h   192.168.2.50   ubuntu   <none>           <none>
kube-system   kube-flannel-ds-arm64-bcxg8      1/1     Running   0          11h   192.168.2.50   ubuntu   <none>           <none>
kube-system   kube-proxy-db2mg                 1/1     Running   0          11h   192.168.2.50   ubuntu   <none>           <none>
kube-system   kube-scheduler-ubuntu            1/1     Running   0          11h   192.168.2.50   ubuntu   <none>           <none>
```
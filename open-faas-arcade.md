[23:12:49]ubuntu@ubuntu:(192.168.2.50)~$ curl -sL https://cli.openfaas.com | sudo sh

```
Finding latest version from GitHub
0.12.9
Downloading package https://github.com/openfaas/faas-cli/releases/download/0.12.9/faas-cli-arm64 as /tmp/faas-cli-arm64
Download complete.

Running with sufficient permissions to attempt to move faas-cli to /usr/local/bin
New version of faas-cli installed to /usr/local/bin
Creating alias 'faas' for 'faas-cli'.
  ___                   _____           ____
 / _ \ _ __   ___ _ __ |  ___|_ _  __ _/ ___|
| | | | '_ \ / _ \ '_ \| |_ / _` |/ _` \___ \
| |_| | |_) |  __/ | | |  _| (_| | (_| |___) |
 \___/| .__/ \___|_| |_|_|  \__,_|\__,_|____/
      |_|

CLI:
 commit:  40555282492b1f7cfdb10d801fcdce251360ec25
 version: 0.12.9
```
[23:19:02]ubuntu@ubuntu:(192.168.2.50)~$ curl -SLsf https://dl.get-arkade.dev/ | sudo sh
```
aarch64
Downloading package https://github.com/alexellis/arkade/releases/download/0.6.12/arkade-arm64 as /tmp/arkade-arm64
Download complete.

Running with sufficient permissions to attempt to move arkade to /usr/local/bin
New version of arkade installed to /usr/local/bin
Creating alias 'ark' for 'arkade'.
            _             _
  __ _ _ __| | ____ _  __| | ___
 / _` | '__| |/ / _` |/ _` |/ _ \
| (_| | |  |   < (_| | (_| |  __/
 \__,_|_|  |_|\_\__,_|\__,_|\___|

Get Kubernetes apps the easy way

Version: 0.6.12
Git Commit: 0415b5fa9d0a6740feb3d9093b7555d38c7e1a51
[23:19:24]ubuntu@ubuntu:(192.168.2.50)~$ arkade install openfaas
Using kubeconfig: /home/ubuntu/.kube/config
Node architecture: "arm64"
Client: "aarch64", "Linux"
2020/09/11 23:19:52 User dir established as: /home/ubuntu/.arkade/
https://get.helm.sh/helm-v3.2.4-linux-arm.tar.gz
/tmp/linux-arm linux-arm/
/tmp/helm linux-arm/helm
/tmp/README.md linux-arm/README.md
/tmp/LICENSE linux-arm/LICENSE
2020/09/11 23:20:19 extracted tarball into /tmp: 3 files, 0 dirs (26.806610235s)
Downloaded to:  /home/ubuntu/.arkade/bin/helm helm
"openfaas" has been added to your repositories

VALUES values-arm64.yaml
Command: /home/ubuntu/.arkade/bin/helm [upgrade --install openfaas openfaas/openfaas --namespace openfaas --values /tmp/charts/openfaas/values-arm64.yaml --set serviceType=NodePort --set clusterRole=false --set openfaasImagePullPolicy=IfNotPresent --set basicAuthPlugin.replicas=1 --set gateway.replicas=1 --set ingressOperator.create=false --set basic_auth=true --set gateway.directFunctions=true --set operator.create=false --set faasnetes.imagePullPolicy=Always --set queueWorker.replicas=1 --set queueWorker.maxInflight=1]
Release "openfaas" does not exist. Installing it now.
NAME: openfaas
LAST DEPLOYED: Fri Sep 11 23:20:26 2020
NAMESPACE: openfaas
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that openfaas has started, run:

  kubectl -n openfaas get deployments -l "release=openfaas, app=openfaas"
=======================================================================
= OpenFaaS has been installed.                                        =
=======================================================================
```
# Get the faas-cli
curl -SLsf https://cli.openfaas.com | sudo sh

# Forward the gateway to your machine
kubectl rollout status -n openfaas deploy/gateway

kubectl port-forward -n openfaas svc/gateway 8080:8080 &

# If basic auth is enabled, you can now log into your gateway:
PASSWORD=$(kubectl get secret -n openfaas basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode; echo)
echo -n $PASSWORD | faas-cli login --username admin --password-stdin

faas-cli store deploy figlet
faas-cli list

# For Raspberry Pi
faas-cli store list \
 --platform armhf

faas-cli store deploy figlet \
 --platform armhf

# Find out more at:
# https://github.com/openfaas/faas

Thanks for using arkade!
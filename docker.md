

# cgroups for docker


**[01:08:46]ubuntu@ubuntu:(192.168.2.50)~$** sudo cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF

```
-bash: /etc/docker/daemon.json: Permission denied
```
sudo vim  /etc/docker/daemon.json
```
{
     "exec-opts": ["native.cgroupdriver=systemd"],
     "log-driver": "json-file",
     "log-opts": {
       "max-size": "100m"
     },
     "storage-driver": "overlay2"
}
```
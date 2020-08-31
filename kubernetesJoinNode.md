# Kubernetes join of a node - when you've tested as master
kubeadm token create --print-join-command

sudo kubeadm reset

sudo kubeadm join 192.168.2.50:6443 --token s63hy4.783nizayh9qmz4st     --discovery-token-ca-cert-hash sha256:4dabcb401861da90f1909c444203363f283fcc5ece20f891db855c5fc6021591 --node-name ubuntu51
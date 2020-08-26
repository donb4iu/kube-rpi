
# [Configure SSH](https://github.com/mhausenblas/kube-rpi#4-configure-ssh)

## ssh ubuntu@192.168.2.50
The authenticity of host '192.168.2.50 (192.168.2.50)' can't be established.
ECDSA key fingerprint is SHA256:JGzL6BVjcsgQXwtf8KGEwNWF/mh/hYBcGuyPC8uCxN0.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.2.50' (ECDSA) to the list of known hosts.
ubuntu@192.168.2.50's password:
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-1015-raspi aarch64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

```
  System information as of Wed Aug 26 02:24:24 UTC 2020

  System load:           0.41
  Usage of /:            6.5% of 28.96GB
  Memory usage:          3%
  Swap usage:            0%
  Temperature:           44.3 C
  Processes:             140
  Users logged in:       1
  IPv4 address for eth0: 192.168.2.50
  IPv6 address for eth0: 2606:a000:4c84:bcf0:dea6:32ff:febb:c8da


0 updates can be installed immediately.
0 of these updates are security updates.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

Last login: Wed Aug 26 02:22:51 2020
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
```

## RPI_SSH_KEY_TARGET=192.168.2.50
## ssh-keygen -b 2048 -t rsa -f $RPI_SSH_KEY_TARGET -q -N ""
##ssh-copy-id -i $RPI_SSH_KEY_TARGET.pub ubuntu@$RPI_SSH_KEY_TARGET
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "192.168.2.50.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys

ubuntu@192.168.2.50's password:

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'ubuntu@192.168.2.50'"
and check to make sure that only the key(s) you wanted were added.

## mv $RPI_SSH_KEY_TARGET* ~/.ssh/

# [Configure SSH](https://github.com/mhausenblas/kube-rpi#4-configure-ssh)

ubuntu@ubuntu:/etc/ssh$ sudo vim ssh_config
PasswordAuthentication no

## ssh ubuntu@192.168.2.50
## ssh ubuntu@192.168.2.51

[16:36:55]**donbuddenbaum@donbs-iMac:~$** ls -l ~/.ssh/id_*.pub
```
ls: /Users/donbuddenbaum/.ssh/id_*.pub: No such file or directory
```
[16:37:01]**donbuddenbaum@donbs-iMac:~$** ls -l ~/.ssh/*.pub
```
-rw-r--r--@ 1 donbuddenbaum  staff   416B Aug 25 22:26 /Users/donbuddenbaum/.ssh/192.168.2.50.pub
-rw-r--r--  1 donbuddenbaum  staff   416B Aug 26 16:12 /Users/donbuddenbaum/.ssh/192.168.2.51.pub
```
[16:37:17]**donbuddenbaum@donbs-iMac:~$** ssh-keygen -t rsa -b 4096 -C "donbuddenbaum@donbs-iMac"
```
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/donbuddenbaum/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/donbuddenbaum/.ssh/id_rsa.
Your public key has been saved in /Users/donbuddenbaum/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:4+8+jbjhDiKgJr4JvLfZVc66TjNn84a7mWg9yk2Qkho donbuddenbaum@donbs-iMac
The key's randomart image is:
+---[RSA 4096]----+
|                 |
|                 |
|                 |
|      . .        |
|.  E o oS.       |
|o.  o ..=.       |
|+o... .=+O.o     |
|= ooo.++@*B..    |
| =oo..oO*XOo     |
+----[SHA256]-----+
```
[16:39:36]**donbuddenbaum@donbs-iMac:~$** ls ~/.ssh/id_*
```
/Users/donbuddenbaum/.ssh/id_rsa      /Users/donbuddenbaum/.ssh/id_rsa.pub
```
[16:40:02]**donbuddenbaum@donbs-iMac:~$** ssh-copy-id ubuntu@192.168.2.51
```
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/donbuddenbaum/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ubuntu@192.168.2.51's password:

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'ubuntu@192.168.2.51'"
and check to make sure that only the key(s) you wanted were added.
```
[16:41:26]**donbuddenbaum@donbs-iMac:~$** ssh ubuntu@192.168.2.51
```
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-1015-raspi aarch64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed Apr  1 18:09:28 UTC 2020

  System load:  0.0               Temperature:           43.8 C
  Usage of /:   6.4% of 28.96GB   Processes:             130
  Memory usage: 3%                Users logged in:       1
  Swap usage:   0%                IPv4 address for eth0: 192.168.2.51


0 updates can be installed immediately.
0 of these updates are security updates.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings


Last login: Wed Apr  1 17:55:48 2020 from 192.168.2.94
```
ubuntu@ubuntu:~$ exit
# Red Hat Lab for Poor-man

Not everyone will have `$` to afford expensive Red Hat subscription :(

This set-up is trying to mimic Red Hat Online learning lab as close as possible.

For those who taking RHCSA, RHCE, this lab is for you!

## Requirements

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- axel *(Optional, to speed up base image download)*

## What will you get ?
2 VM created in Virtual Box using CentOS 7 image. Default user is `student` with sudo-capability.

```bash
- server.example.com[172.25.1.10]:
  \- /dev/vda [40GB]
  \- /dev/vdb [2GB] 
- desktop.example.com [172.25.1.11]
  \- /dev/vda [40GB]
```


## Download and import base image

Download and import Vagrant base box. You only need to do this once.

```bash
axel -a -n10 "https://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-1803_01.VirtualBox.box"
vagrant box add CentOS-7-x86_64-Vagrant-1803_01.VirtualBox.box  --name "centos/7"
rm CentOS-7-x86_64-Vagrant-1803_01.VirtualBox.box
```

## Initialise lab

```bash
# Create lab
vagrant up

# Login to server and desktop
vagrant ssh server
vagrant ssh desktop
```

If you are done with the lab, destroy everything by

```bash
vagrant destroy -f
```



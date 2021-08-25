## k8s-raspberry
---

This repository contains the code for install and configure a Kubernetes cluster with kubeadm in 3 Raspberry's Pi 4 running under Ubuntu Server.

### Requirements:

<img src="https://img.shields.io/badge/Ansible-2.10-grey?style=flat-square&logo=ansible" alt="Ansible 2.10"/>
<img src="https://img.shields.io/badge/Ubuntu-21.04-orange?style=flat-square&logo=ubuntu" alt="Ubuntu 21.04"/>

I'll presume that you use a linux. If you use another system, check the equivalent commands. You can contribute with this repo to add another distro...

You can see how install Ubuntu on Raspberry's here: 

https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#1-overview

I use this image: https://ubuntu.com/download/raspberry-pi/thank-you?version=21.04&architecture=server-arm64+raspi

After burn Ubuntu image to SDCard, you can define a static ip address. 
Edit the `network-config` on the system-boot partition, like as: 

```yaml
version: 2
ethernets:
  eth0:
    dhcp4: false
    optional: true
    addresses:
      - 10.100.1.11/24 
    gateway4: 10.100.1.1
    nameservers:
      addresses: [8.8.8.8, 1.1.1.1]
```

Define the `address` and `gateway4` as you prefer, but remember define the address different for each pi. 

And you can configure a default password to SSH, creating a file `ssh.txt` on the boot partition. Use this password to connect after the boot. 

Obs.: On first time you connect in the pi, you need change the password. 

Also, I recommend to configure SSH access with  SSH Keys to your raspberry's:

- Create a SSH key:

```shell
ssh-keygen -f ~/.ssh/rasps-k8s -C "Key for access raspberrys" -P ""
```

So, register your public SSH key in your raspberry's: 

```
ssh-copy-id -i ~/.ssh/rasps-k8s.pub ubuntu@10.100.1.11
```

Test your SSH access in all nodes, no password will be required.

Next, i recommend you set hostname different to each Pi.

### Ansible Roles

I prepared five roles: 
  - configure_node: Enable kernel modules, firewall rules and another linux changes.
  - install_containerd: No Docker is required, just containerd. This role install it.
  - install_k8s: Install k8s with kubeadm and Helm  
  - init_cluster: Initialize cluster and install pod network
  - join_workers: Join node workers to cluster
  - install_monit_tools: Install helm chart for Prometheus Stack
  - Who's next? 

Check each role folder for more details...

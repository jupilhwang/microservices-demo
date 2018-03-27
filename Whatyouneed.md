# Minikube 
or
# Creating the Kubernetes clsuter on Virtualbox with Vagrant

## tl;dr
- Install VirtualBox
- Install Vagrant
- Clone the GitHub repository git clone https://github.com/oracle/vagrant-boxes
- Run vagrant up master; vagrant ssh master
- Within the master guest, run as root: /vagrant/scripts/kubeadm-setup-master.sh
- You will be asked to log in to the Oracle Container Registry
- Run vagrant up worker1; vagrant ssh worker1
- Within the worker1 guest, run as root: /vagrant/scripts/kubeadm-setup-worker.sh
- You will be asked to log in to the Oracle Container Registry
- Repeat the last 2 steps for worker2

## What you need
1. [Virtualbox](https://www.virtualbox.org/wiki/Downloads)
2. [Vagrant](https://www.vagrantup.com/downloads.html)
3. Creating a user on https://container-registry.oracle.com
4. Cloning the [Virtualbox Vagrant Github repo](https://github.com/oracle/vagrant-boxes)

## Creating the Kubernetes cluster on Virtualbox with Vagrant
### Cloning the Github repo
```sh
git clone https://github.com/oracle/vagrant-boxes
```

### Creating the Kubernetes master
```sh
cd vagrant-boxes/Kubernetes
vagrant up master
```

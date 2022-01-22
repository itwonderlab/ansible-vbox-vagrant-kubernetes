# Ansible VirtualBox Vagrant Kubernetes 1.22 Containerd and Istio Tutorial (1 master N nodes)
## Building a Kubernetes Cluster with Vagrant and Ansible

Tutorial with full source code explaining **how to create a Kubernetes cluster with Ansible and Vagrant** for local development.

See https://www.itwonderlab.com/en/ansible-kubernetes-vagrant-tutorial/

* 22 Dec 2019: Add information about using a Private Docker Registry as suggested by Brian Quandt.
* 4 Nov 2019: Install and publish Kubernetes Dashboard under vagrant, with help from Alex Alongi. Add prerequisites section as requested
* 26 Sep 2019: Update Calico networking and network security to release 3.9
* 6 June 2019: Fix issue: kubectl was not able to recover logs. See new task “Configure node-ip … at kubelet”.
* 10 Jul 2020:
        Update prerequisites to latest releases
        It now takes above 2 minutes
        Change selection of hosts from Ansible groups to host-name pattern (hosts: k8s-m-* and hosts: k8s-n-*)
* 3 Aug 2020: Allow different amount of CPU and MEM for master and nodes
* 10 June 2021: Update host software dependencies (no changes in ansible or vagrant)
* 16 August 2021: Update Ansible playbooks to use containerd instead of Docker (Kubernetes is deprecating Docker as a container runtime after v1.20.). 


------------------

## For Windows users
It is possible to execute the provisioning by leveraging the WSL2 sharing functionalities of Windows. Take a look [here](https://gist.github.com/pr3l14t0r/8b350fc7052ccee30a456596fa017c33) for further requirements and explanation.
Uncomment the Windows related lines in the Vagrantfile in order to inject a ssh key from your WSL2 distribution into the VMs.

## Creación de un Clúster de Kubernetes 1.22 Containerd e Istio usando Vagrant y Ansible (1 maestro N nodos)

Creación de un **clúster Kubernetes con múltiples nodos usando Vagrant, Ansible y Virtualbox**. Especialmente indicado para entornos de desarrollo local realistas.

See https://www.itwonderlab.com/es/cluster-kubernetes-vagrant-ansible/

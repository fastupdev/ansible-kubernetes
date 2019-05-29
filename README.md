# Ansible Kubernetes Playbook

### Introduction
The Ansible Kubernetes Playbook is an introductory version to install a single master and multiple worker nodes Kubernetes cluster in the following operating systems.
1. Red Hat Linux
2. Ubuntu (work in progress)
3. CentOS (work in progress)
4. Windows (work in progress)
**Note**: At the moment the playbook can only install on Red Hat Linux machines, rest of the playbooks are still in progress.

### Prerequisites
To run the above playbook, following are the prerequisites before even we run the playbook,

1. Provision servers with the [minimum](https://kubernetes.io/docs/setup/independent/install-kubeadm/#before-you-begin) CPUs, Memory, Storage and Network Setup available.
2. Make sure there is python already installed on the provisioned servers with the right [interpreter](https://docs.ansible.com/ansible/latest/reference_appendices/python_3_support.html#python-3-support).

### Playbook Pre-configuration
To install the playbook follow the below steps,

1. Clone the Ansible Kubernetes Playbook 
2. Once the servers are provisioned, make sure to add the Master Node IP or Hostname in the _masternode_ group and Worker Node IP or Hostname in the _workernode_ group in the **hosts** file.
``` 
[masternodes]
master.hostname/IP

[workernodes]
worker1.hostname/IP
worker2.hostname/IP 
```
3. Make sure to replace the _remote\_user_ value in the **ansible.cfg** file.
4. Add the _ansible\_ssh\_private\_key\_file_ or _ansible\_password_ for the _remote\_user_ in the **hosts** file.
5. Add the _ansible\_become\_password_ in the **hosts** for privilage escaltion.

### Installation

Once all the configurations are in the right place, run the following command

``` ansible-playbook main.yml ```

Sit back and relax for the playbook to finish with no errors.  :smile:!!!

**Note**: This playbook is tested on Red Hat Linux servers.
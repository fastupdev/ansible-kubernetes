# Ansible Kubernetes Playbook

### Introduction
The Ansible Kubernetes Playbook is an early version to install HA Kubernetes cluster in the following operating systems.
1. Red Hat Linux
2. Red Hat CentOS Linux
2. Ubuntu 
3. Debian
5. Windows (_work in progress_)

**Note**: Currently the playbook can only install a single master Kuberentes cluster on Red Hat Linux, Red Hat CentOS Linux machines, Ubuntu and Debian it is in progress for the Windows Operating Systems.

### Prerequisites
To run the playbook, the following are the prerequisites before even we run the playbook,

1. Provision servers with the [minimum](https://kubernetes.io/docs/setup/independent/install-kubeadm/#before-you-begin) CPUs, Memory, Storage and Network Setup available.
2. Make sure there is a python [interpreter](https://docs.ansible.com/ansible/latest/reference_appendices/python_3_support.html#python-3-support) installed on the provisioned servers. 

### Playbook Pre-configuration
Follow the below steps to set up and configure the environment to run the installation playbook,

#### Hosts Configuration 
To configure the hosts in the playbook, clone the **Ansible Kubernetes Playbook** repository.

Once the servers are provisioned, add the following information in the **hosts** file, 
1. **Master Node IP or Hostname** in the **_masternode_ group**
2. **Worker Node IP or Hostname** in the **_workernode_ group**

``` 
[masternodes]
master.hostname/IP

[workernodes]
worker1.hostname/IP
worker2.hostname/IP 
```

#### User Configuration
After the Hosts Configuration, add the following in the **hosts** file to run playbook with a specific user, 
1. Replace the **_remote\_user_** value in the **ansible.cfg** file.
2. Add the **_ansible\_ssh\_private\_key\_file_** or **_ansible\_password_** for the **_remote\_user_** in the **hosts** file.
3. Add the **_ansible\_become\_password_** in the **hosts** file for privilage escaltion.

#### Network Configuration
**Ansible Kubernetes Playbook** can configure Kubernetes CNI plugin with either Flannel, Calico or Canal in the **hosts** file,
```CNI_network_type= flannel|calico|canal ```

#### Quick Note on CNI Plugins
**Flannel** is a straightforward plugin that configures a layer 3 IPv4 overlay network. Flannel uses Docker bridge for the Pods to communicate within the same host, while pods on different hosts communicate using flanneld with a default VXLAN by encapsulating the traffic in UDP packets to route to the appropriate destination.

**Calico** is most flexible and popular Kubernetes CNI plugin that configures a layer 3 network that uses the BGP(border gateway protocol) routing protocol to route packets between hosts by eliminating an extra layer of encapsulation. Calico is more easy for conventional debugging standard debugging tools when there is a network problem. Calico can also integrate with a _service mesh_ like, **Istio** to provide extra security and control over the network policy.

**Canal** is a mix of Calico and Flannel, which means Canal configures a layer 3 IPv4 overlay network from Flannel and the network policy capabilities layered from Calico, which is also the right way for teams to experiment.

### Installation

Once all the configurations are in the right place, run the following command to install Kubernetes,

``` ansible-playbook main.yml ```

Keeping time constraint in mind while retrying the playbook, add the ```--skip-tags=common-tasks``` to skip the tasks of the common packages.

Sit back and relax for the playbook to finish with no errors :smile:!!!


**Note**: This playbook is tested on Red Hat Linux, CentOS Linux servers, Ubuntu and Debian Operating Systems.
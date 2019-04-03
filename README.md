# ansible-role-avicontroller-kvm
Ansible Role to setup Avi Controller on KVM

Requirements
------------
 - python >= 2.6
 - avisdk : It can be installed by `pip install avisdk --upgrade`
 - avinetworks.avisdk : It can be installed by `ansible-galaxy install -f avinetworks.avisdk` 

Role Variables
--------------

| Variable | Required | Default | Comments |
|----------|----------|---------|----------|
|kvm_vm_hostname|Yes||Name for VM|
|kvm_vm_base_img|No|It will take from hosts root dir|controller.qcow2 file|
|kvm_vm_vcpus|No|8|How many cpus the controller will use.|
|kvm_vm_ram|No|16384MB|How much memory the controller will use.|
|kvm_vm_os_disk_size|Yes|40|How much disk size the controller will use.|
|host_mgmt_intf|Yes||host management interface name|
|ctrl_mgmt_ip|Yes||Management Ip for the controller|
|ctrl_mgmt_mask|Yes||Subnet mast for the controller|
|ctrl_default_gw|Yes||Default gateway for controller|
|state|Yes|present|If present then it will create controller and for absent it will destroy controller.|
|kvm_pinning|Yes||If you want to enable pinning CPU for the VM|
|kvm_host_ip|Yes||KVM host IP|
|kvm_host_username|Yes||KVM host Username|
|kvm_host_password|Yes||KVM host Password|


### Standard Example
```
- hosts: kvm
  vars:
    kvm_vm_hostname: "ctrl1"
    host_mgmt_intf: eno1.100
    ctrl_mgmt_ip: 10.130.5.12
    ctrl_mgmt_mask: 255.255.255.0
    ctrl_default_gw: 10.130.5.1
    kvm_pinning: true
    kvm_host_ip: "10.130.5.44"
    kvm_host_username: "root"
    kvm_host_password: "password"
  tasks:
    - name: Create KVM VM
      include_role:
        name: ansible-avicontroller-kvm
```

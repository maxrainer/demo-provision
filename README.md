# **Ansible - AWS virtual Network Topology**

## **Overview**
This Ansible Playbook builds virtual networks on AWS Cloud. Real world WAN and security topologies are supported. 
It's very simple to add currently non-supported network devices. 

## **Features**
First a VPC with multiple subnets is created. 
Routers, Firewalls can have multiple interfaces in different subnets. 

### **Supported and tested devices**
##### **Routers**
* Cisco CSR 1000v
* Juniper vMX
##### **Firewalls**
* Palo Alto 
* Juniper vSRX
* Fortigate 
##### **Linux Servers**
* Ubuntu 18
* RHEL 7/8
* Centos 7
##### **Special Servers**
* Ansible Tower
* Bastion Server (SSH proxy, squid)

## **Usage**
* find variable definitions here:
[variables](./roles/aws-provision/defaults/main.yml)
* define your network topology in ./group_vars/aws.yml
[aws.yml](./group_vars/aws.yml) 
* start AWS Cloud provisioning  
`ansible-playbook -i localhost.inv provision.yml`
* define your Ansible Tower variables in ./group_vars/function_tower.yml
[function_tower.yml](./group_vars/function_tower.yml)
* start Post Installation Tasks  
  `ansible-playbook -i lab.aws_ec2.yml post.yml`
* Teardown everything from AWS Cloud  
  `ansible-playbook -i localhost.inv -t teardown --skip-tags=always provision.yml`

## **ready to use Examples**

[simple WAN - 3 Cisco IOS Router](./docs/RT3_WAN.md)

## **further informations**
#### **installed Projects on Tower**
[network-labs](https://github.com/maxrainer/ansible-network-labs)

#### **howto add new Devices**
* device definitions can be found in
[./roles/aws-provision/vars/main.yml](./roles/aws-provision/vars/main.yml)

## **Prerequests**
* ansible >= 2.9
* boto3 >= 1.12
* genie, pyats >= 20.1 
* paramiko >= 2.7.1

## **open caveats**
* only Region europe-central1 supported
* dynamic DNS support
* SQUID reverse Proxy on bastion
* easy SSH to devices through bastion
* F5 example
* dual Firewall example
* molecule testing
* template module bug (can't set venv) (https://github.com/ansible/ansible/issues/68492)
* make roles independent from playbook

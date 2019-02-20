# ONTAP Select

There are 2 Ansible Playbooks in this repository, one for the installation of an ONTAP Select cluster and one to destroy an ONTAP Select cluster.

Requirements:
- ONTAP Deploy 2.8 or newer
- The vCenter Server needs to have already been added to the Credentials Manager in Deploy
- NetApp Ansible Modules only running with [NetApp Lib](https://pypi.org/project/netapp-lib/)

Known bugs/issues and Open RFEs

- Add the possibility to use licenses (currently it only installs eval installations)
- Remove the need to added capacity to each node and group the HA pairs together
- Add possibility to convert the enter the capacity needed in GB instead of bytes (which is required by Deploy)
- The Delete ONTAP Select playbook has not yet been worked on and will not yet work!

How to start

We suggest to create groupvars to specify you environment specific parameters e.g. credentials, ONTAP Deploy Instance, network-configuration, ...

First create an inventory file `inventory/hosts`:
```
[adminstation]
localhost
```

Second create a vars file to configure your environment:

The following example shows `inventory/group_vars/adminstation/all/vars.yml`:

```
deploy_name: "192.168.5.23"
otd_user: "admin"
otd_password: "{{ otd_password_vault }}"
ots_password: "{{ ots_password_vault }}"

# ----- Cluster Specific -----
new_cluster_node_num: "2"
new_cluster_name: "cl01"
ontap_version: "9.4P4"
license_code: ""
new_cluster_gateway: "192.168.100.1"
new_cluster_ip: "192.168.5.101"
new_cluster_netmask: "255.255.255.0"
ntp_servers:
  - "192.168.5.1"
domain_names:
  - "assembling.localdomain"
dns_ips:
  - "192.168.5.1"
mgmt_net: "mgmt"
data_net: "data"
int_net:  "internal"

# ----- Node Specific -----
instance_type: "small"
node_ips:
  - "192.168.5.102"
  - "192.168.5.103"
storagepool_capacity:
  - 2100000000000
  - 2100000000000
storagepool_name:
  - "esxi03_ds1"
  - "esxi01_ds1"

# ----- vCenter Specific -----
vcenter_server: ""
# ----- Host Specific -----
host_names:
  - "192.168.5.22"
  - "192.168.5.20"
```

You can then run the playbook like this:

```
ansible-playbook  -i inventory/hosts playbooks/create_cluster.yml
```


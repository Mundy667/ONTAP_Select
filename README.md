# ONTAP Select

There are 2 Ansible Playbooks in this repository, one for the installation of an ONTAP Select cluster and one to destroy an ONTAP Select cluster.

Requirements:
- ONTAP Deploy 2.8 or newer
- The vCenter Server needs to have already been added to the Credentials Manager in Deploy
- NetApp Ansible Modules only running with NetApp lib [https://pypi.org/project/netapp-lib/|pip install netapp-lib]

Known bugs/issues and Open RFEs

- Add the possibility to use licenses (currently it only installs eval installations)
- Remove the need to added capacity to each node and group the HA pairs together
- Add possibility to convert the enter the capacity needed in GB instead of bytes (which is required by Deploy)
- The Delete ONTAP Select playbook has not yet been worked on and will not yet work!

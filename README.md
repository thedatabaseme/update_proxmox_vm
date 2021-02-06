Update_Proxmox_VM
=========

This Playbook enables you to update / patch all your VMs on your Proxmox Cluster.

Requirements
------------

- Ansible 2.7

Playbook Variables
--------------

- proxmox_api_user (Default root@pam): Proxmox API Username
- proxmox_api_password (Default Start123): Password of the API User
- proxmox_api_host (Default pvehost1): Hostname of the Proxmox Server
- proxmox_api_port: (Default 8006): Proxmox API Port (normally 8006)
- boot_time: (Default 180): Sleep Time for VM to boot
- vm_list: A List of VMs you want to patch. (Must be the same Name than in the Inventory File)

More Informations
------------

Be aware, that this role will run at the localhost (Ansible Controlhost) by default. All Proxmox Tasks will be made by REST API to the Proxmox Server.
All VMs you want to patch in this process must be found in the Inventory you mention when running the Playbook. There is an Example Inventory File included. (hosts_example)
All VMs in your list will be patched one after another.

Attention: At the moment, when you run multiple Proxmox Cluster Nodes, all Nodes must be up and running. Else there will be an error when getting the VM Status because the Name of the VM is not resolveable.

Example Playbook
----------------

There is an example Playbook included update_proxmox_vm.yml

An example Playbook Call looks like this. Ofcourse you may want to specify the Variables within your Playbook or within your Inventory:

    - ansible-playbook -i hosts_example -e '{"vm_list": ["vm1", "vm2"], "proxmox_api_host": "srvoffice2.home.lab", "proxmox_api_password": "Evenmoresecret"}' update_proxmox_vm.yml  

Author Information
------------------

This Role is created by P. Haberkern (theoracleme)

Update_Proxmox_VM
=========

This Playbook enables you to update / patch all your VMs on your Proxmox Cluster.

Requirements
------------

- Ansible 2.8

Playbook Variables
--------------

- proxmox_api_user (Default root@pam): Proxmox API Username
- proxmox_api_password (Default Start123): Password of the API User
- proxmox_api_host (Default pvehost1): Hostname of the Proxmox Server
- proxmox_api_port: (Default 8006): Proxmox API Port (normally 8006)
- boot_time: (Default 180): Sleep Time for VM to boot
- dist_upgrade: (Default false): Controls if apt dist-upgrade operation should be done or not
- vm_list: A Dictionary of VMs you want to patch. (Must be the same Name than in the Inventory File). You can specify if a Snapshot should be taken after Patching is done. (snapshot: true; see Examples in the Playbook) Also you can specify, if you want to reboot the VM after an Update if needed (working only for Ubuntu / Debian Systems) by specifying the reboot_if_required: true Variable (see Examples in the Playbook)

  Example VM List:

      vm_list:
      - vm_name: myShinyVM1
      - vm_name: myShinyVM2
        snapshot: true
        reboot_if_required: true

More Information
------------

Be aware, that this role will run at the localhost (Ansible Controlhost) by default. All Proxmox Tasks will be made by REST API to the Proxmox Server.
All VMs you want to patch in this process must be found in the Inventory you mention when running the Playbook. There is an Example Inventory File included. (hosts_example)
All VMs in your list will be patched one after another.

Attention: At the moment, when you run multiple Proxmox Cluster Nodes, all Nodes must be up and running. Else there will be an error when getting the VM Status because the Name of the VM is not resolveable.

Example Playbook
----------------

There is an example Playbook included update_proxmox_vm.yml

An example Playbook Call looks like this. Ofcourse you may want to specify the Variables within your Playbook or within your Inventory:

    - ansible-playbook -i hosts_example -e '{"proxmox_api_host": "srvoffice2.home.lab", "proxmox_api_password": "Evenmoresecret"}' update_proxmox_vm.yml  

Maybe you want to specify the VM Dictionary in a separate File. Then you can call the Playbook like so:

    - ansible-playbook -i hosts -e "@vm_list_to_patch.yml" -e '{"proxmox_api_host": "srvoffice2.home.lab", "proxmox_api_password": "Evenmoresecret"}' update_proxmox_vm/update_proxmox_vm.yml

Author Information
------------------

This Role is created by P. Haberkern (thedatabaseme)

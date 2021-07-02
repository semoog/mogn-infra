# mogn-infra
Homelab cluster automation playbook.

## Currently:

- Configures and starts an HA etcd cluster based on an arbitrary number of nodes

## Requirements

- a control node (Ansible installed, this repo cloned) with ssh access to the host nodes
- a `hosts` file setup in the following way:
    
        [cluster-name]
        node-1 ip=<node-1-ip>
        node-2 ip=<node-2-ip>
        node-3 ip=<node-3-ip>
        ...
        
## Running the playbook

    ansible-playbook provision.yml

## TODO

- HA k3s automation
- HA rke automation

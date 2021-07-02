# mogn-infra
Homelab cluster automation playbook.

## Currently:

- Configures and starts an HA [etcd](https://etcd.io/) cluster based on an arbitrary number of nodes

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

- ~~Part 1 - HA etcd~~
    - 3e3fea6ae2b58a9b43c9fb29cf19efe2f1a7177e
- Part 2 - HA k3s
- Part 3 - HA rke

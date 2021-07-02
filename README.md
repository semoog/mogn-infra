# mogn-infra
Homelab k3s cluster automation.

## Currently:

    - Configures and starts an HA etcd cluster based on an arbitrary number of nodes

## Requirements

- a `hosts` file setup in the following way:
    
        [cluster-name]
        node-1 ip=<node-1-ip>
        node-2 ip=<node-2-ip>
        node-3 ip=<node-3-ip>

## TODO

- HA k3s automation
- HA rke automation

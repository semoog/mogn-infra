# mogn-infra
<br>
Homelab cluster automation playbook.

Configures and spins up an HA [etcd](https://etcd.io/) + [k3s](https://k3s.io/) cluster based on an arbitrary number of nodes.
<br>
<br>

## Requirements

- a control node
    - [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed
    - [cfssl](https://github.com/cloudflare/cfssl) installed (used to generate certs)
    - ssh access to the host nodes (update the `user` field in `provision.yml` to match)
- a `hosts` file (can be created with `ansible-playbook init.yml`):
    
        [servers]
        node-1 ip=<node-1-ip>
        node-2 ip=<node-2-ip>
        node-3 ip=<node-3-ip>
        

        [agents]
        node-4 ip=<node-4-ip>
- a `vars/secrets.yml` file (can be created with `ansible-playbook init.yml`):

        ---

        K3S_TOKEN: "<CUSTOM_TOKEN>"
<br>

## Running the playbook(s)
<br>

### Initialize `hosts` and `vars/secrets.yml` files (optional): 
    
    ansible-playbook pre.yml

Don't forget to update the values to fit your cluster.

_---_

### Main provisioning playbook:

    ansible-playbook provision.yml

_---_

### Automatically set kubeconfig on control node (unix):

    ansible-playbook post.yml
<br>

## TODO

- ~~Part 1 - HA etcd~~
    - merged with [3e3fea6](https://github.com/semoog/mogn-infra/commit/3e3fea6ae2b58a9b43c9fb29cf19efe2f1a7177e)
- ~~Part 2 - HA k3s~~
    - merged with [PR - k3s roles](https://github.com/semoog/mogn-infra/pull/1)
- Part 3 - HA rke

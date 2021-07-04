# mogn-infra
<br>
Homelab cluster automation playbook.

Configures and spins up a HA [etcd](https://etcd.io/), [k3s](https://k3s.io/), [rancher](https://rancher.com/products/rancher/) cluster based on an arbitrary number of nodes.

HA assuming a minimum of 2 server nodes.
<br>
<br>
![example layout](mogn-infra_example-layout.png)
<br>
<br>
*note: rancher / k3s agent role is available, I just don't have any in my cluster yet*

## Requirements

- a control node
    - [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed
    - [cfssl](https://github.com/cloudflare/cfssl) installed (used to generate certs)
    - [helm](https://helm.sh/docs/intro/install/) installed
    - ssh access to the host nodes (update the `user` field in `provision.yml` to match)
- 1+ server / agent node
- *optional:* 1+ external load balancer node, otherwise [traefik](https://doc.traefik.io/traefik/) will be used internally (ships with k3s)
- a `hosts` file (template can be created with `ansible-playbook init.yml`):
    
        [servers]
        node-1 ip=<node-1-ip>
        node-2 ip=<node-2-ip>
        node-3 ip=<node-3-ip>

        [agents] <- optional
        node-4 ip=<node-4-ip>

        [load-balancers] <- optional
        lb-1 ip=<lb-1-ip>
- a `vars/secrets.yml` file (template can be created with `ansible-playbook init.yml`):

        ---

        K3S_TOKEN: "<CUSTOM_TOKEN>"
- change the value of `DNS_NAME` and `user` in `provision.yml`
<br>

## Running the playbook(s)
<br>

### Initialize `hosts` and `vars/secrets.yml` files (optional): 

<br>
  
    ansible-playbook init.yml

Don't forget to update the values to fit your cluster.

_---_

### Main provisioning playbook:

<br>

    ansible-playbook provision.yml

<br>

*The default behavior of `provision.yml` is to run the `kubectl.yml` playbook at the end which copies and adds the kubeconfig to the local control node for access to the cluster. If you would like to skip this step append `-e nokubectl=True` to the command e.g:*

    ansible-playbook provision.yml -e nokubectl=True
<br>

## Verifying the cluster
<br>

    source ~/.profile
    
    kubectl get nodes
<br>

Browse to the DNS_NAME url (e.g `rancher.mogn.co`) that you set in the `provision` playbook and you should see the rancher welcome screen.
<br>
<br>

## TODO

- *Part 0 (?) - PXE boot*

- ~~Part 1 - HA etcd~~
    - merged with [3e3fea6](https://github.com/semoog/mogn-infra/commit/3e3fea6ae2b58a9b43c9fb29cf19efe2f1a7177e)

- ~~Part 2 - HA k3s~~
    - merged with [PR - k3s roles](https://github.com/semoog/mogn-infra/pull/1)

- ~~Part 3 - HA rancher~~
    - merged with [PR - rancher role](https://github.com/semoog/mogn-infra/pull/2)

- ~~Part 4 - nginx cluster load balancer~~
    - merged with [PR - nginx lb](https://github.com/semoog/mogn-infra/pull/3)

- Part 5 - TLS

- Part ? - HA load balancing

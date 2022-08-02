# K8s multi node cluster with wasm support

Supported OS:
- Ubuntu 20.04
- Ubuntu 22.04

Container Runtime:
- High-Level: containerd
- Low-Level: crun with WasmEdge Support

# Usage

## Development environment

Before building the cluster, you need to install following:

- Ansible
- VirtulaBox
- Vagrant

Then, in this directory:

1. `vagrant up`
2. `cd ansible`
3. `ansible-playbook -i inventories/vagrant_vm master_playbook.yml`
4. `ansible-playbook -i inventories/vagrant_vm worker_playbook.yml`

When successfully completed, `join-command` is created in `ansible`.

### Run wasm sample app

1. `vagrant ssh master`
2. `kubectl create -f /vm_share/wasm-sample-app.yml`

You can see the output by executing `kubectl logs wasm-sample-app`.

### Note

When `vagrant up`, an error about IP range may be occured like this:

```
The IP address configured for the host-only network is not within the
allowed ranges. Please update the address used to be within the allowed
ranges and run the command again.

  Address: 192.168.50.10
  Ranges: 192.168.56.0/21

Valid ranges can be modified in the /etc/vbox/networks.conf file. For
more information including valid format see:

  https://www.virtualbox.org/manual/ch06.html#network_hostonly
```
You can solve this by adding following line in `/etc/vbox/networks.conf` (you need to create this file if it doesn't exist):

`* 0.0.0.0/0 ::/0`

## Production environment

Before building the cluster, you need to install Ansible.

Then, in this directory:

1. Create an ansible inventory file in `ansible/inventories` (refer to [Ansible Docs] if you don't know inventory file)
3. `cd ansible`
4. Make sure `ansible all -i "path/to/inventory/file" -m ping` is success
5. `ansible-playbook -i "path/to/inventory/file" master_playbook.yml`
6. `ansible-playbook -i "path/to/inventory/file" worker_playbook.yml`


[Ansible Docs]: https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html

# K8s multi node cluster with wasm support

Container Runtime is following:

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

When successfully completed, `join-command` is created in `ansible` but you can remove it.

### Run wasm sample app

1. `vagrant ssh master`
2. `kubectl create -f /vm_share/wasm-sample-app.yml`

You can see the output by executing `kubectl logs wasm-sample-app`.

## Production environment

Coming soon


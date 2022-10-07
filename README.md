
# Vagrantfile and Scripts to Automate Kubernetes Setup

## Prerequisites

1. Working Vagrant setup
2. 8 Gig + RAM workstation as the Vms use 3 vCPUS and 4+ GB RAM

## For MAC/Linux Users

Latest version of Virtualbox for Mac/Linux can cause issues because you have to create/edit the /etc/vbox/networks.conf file and add:
<pre>* 0.0.0.0/0 ::/0</pre>

or run below commands

```shell
sudo mkdir -p /etc/vbox/
echo "* 0.0.0.0/0 ::/0" | sudo tee -a /etc/vbox/networks.conf
```

So that the host only networks can be in any range, not just 192.168.56.0/21 as described here:
https://discuss.hashicorp.com/t/vagrant-2-2-18-osx-11-6-cannot-create-private-network/30984/23

## Usage/Examples

To provision the cluster, execute the following commands.

```shell
git clone https://github.com/dkhachyan/vagrant-kube.git
cd vagrant-kube/kubespray
vagrant up
git clone https://github.com/kubernetes-sigs/kubespray.git
cd kubespray
ansible-playbook -i ../inventory/inventory.ini cluster.yml -b -u vagrant
```

## Set Kubeconfig file variable

```shell
cd vagrant-kube
cd configs
export KUBECONFIG=$(pwd)/config
```

or you can copy the config file to .kube directory.

```shell
cp config ~/.kube/
```

## To destroy the cluster,

```shell
vagrant destroy -f
```

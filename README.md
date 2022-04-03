# MongoDB Docker Swarm, Configured by Ansible
## Prerequisites

Your local dns server should be search datacenter.local on the subnet 172.28.128.1/24. I acheived this by adding `server=/datacenter.local/172.28.128.1#53` to `/etc/NetworkManager/dnsmasq.d/50-datacenter.conf` on Manjaro

## Usage

0. clone this repo and cd into it
1. `vagrant up --parallel --provider=libvirt`
1. `cd ansible`
1. `ansible-playbook -i inventories/virtual_machines.yml deploy_datacenter_base.yml -u root`
1. `ansible-playbook -i inventories/containers/ init_mongo_swarm.yml -u root`

## FAQ

1. Q: What does it do?
    
    A: Exist

2. Q: Anything else?

    A: No
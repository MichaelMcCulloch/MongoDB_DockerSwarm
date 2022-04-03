# MongoDB Docker Swarm, Configured by Ansible
## Prerequisites

Your local dns server should be search datacenter.local on the subnet 172.28.128.1/24. I acheived this by adding `server=/datacenter.local/172.28.128.1#53` to `/etc/NetworkManager/dnsmasq.d/50-datacenter.conf` on Manjaro

## Usage

0. clone this repo and cd into it
1. `vagrant up --parallel --provider=libvirt`
1. `cd ansible`
1. `ansible-playbook -i inventories/ deploy_datacenter_base.yml -u root`
1. `ansible-playbook -i inventories/ init_mongo_swarm.yml -u root`
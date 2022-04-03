# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
    # The most common configuration options are documented and commented below.
    # For a complete reference, please see the online documentation at
    # https://docs.vagrantup.com.
  
    # Every Vagrant development environment requires a box. You can search for
    # boxes at https://vagrantcloud.com/search.
    config.vm.box = "archlinux/archlinux"
    config.ssh.forward_agent = true
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.synced_folder "./data", "/data", type: "rsync", rsync__auto: true, mount_options: ["dmode=777,fmode=777"]
  
    config.vm.provider "libvirt" do |lv|
      lv.memory = 4096
      lv.cpus = 4
      lv.nested = true
    end

    config.vm.network "private_network", 
      :dev => "virbr1", 
      :mode => "bridge", 
      :type => "dhcp", 
      :libvirt__domain_name => "datacenter.local",
      :libvirt__network_name => "datacenter.local",
      :libvirt__network_address => "172.28.128.0/24"

    (1..2).each do |i|
      name = "manager-#{i.to_s.rjust(2, "0")}"

      config.vm.define "#{name}" do |manager_machine|
        manager_machine.vm.hostname = "#{name}"
      end

    end

    (1..3).each do |i|
      name = "data-#{i.to_s.rjust(2, "0")}"

      config.vm.define "#{name}" do |data_machine|
        data_machine.vm.hostname = "#{name}"
      end

    end

    (1..3).each do |i|
      name = "config-#{i.to_s.rjust(2, "0")}"

      config.vm.define "#{name}" do |cfg_machine|
        cfg_machine.vm.hostname = "#{name}"
      end

    end

    (1..2).each do |i|
      name = "router-#{i.to_s.rjust(2, "0")}"

      config.vm.define "#{name}" do |query_router_machine|
      query_router_machine.vm.hostname = "#{name}"
      end

    end



  
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "config.yml"
    end

    config.vm.provision :reload


  end
  
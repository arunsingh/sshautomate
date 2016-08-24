# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
#  config.vm.box = "geerlingguy/ubuntu1404"
  config.vm.box = "centos/7"  
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
#    v.name = "instance"
    v.memory = 512
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

# Instance 1
  config.vm.define :instance1 do |instance1|
    config.vm.hostname = "instance1"
    config.vm.network :private_network, ip: "192.168.33.33"
 # Ansible provisioner for instance1.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
#    ansible.inventory_path = "inventory"
    ansible.sudo = true
  end
 end

# Instance2
  config.vm.define :instance2 do |instance2|
    config.vm.hostname = "instance2"
    config.vm.network :private_network, ip: "192.168.33.34"
# Ansible provisioner for instance2.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.sudo = true
  end
 end


end

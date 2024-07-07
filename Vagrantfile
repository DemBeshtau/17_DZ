# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  #Использовать один ключ для всех хостов
  config.ssh.insert_key = false
  
  config.vm.define "client" do |client|
    client.vm.box = "ubuntu/jammy64"
    client.vm.box_version = "0"
    client.vm.host_name = "client"
    client.vm.network "private_network", ip: "192.168.56.150"
    client.vm.provider "virtualbox" do |v|
      config.vm.synced_folder ".", "/vagrant", disabled: true
      v.gui = false
      v.memory = 1024
      v.cpus = 1
    end
  end
  
  config.vm.define "backup" do |backup|
    backup.vm.box = "ubuntu/jammy64"
    backup.vm.box_version = "0"
    backup.vm.host_name = "backup"
    backup.vm.network "private_network", ip: "192.168.56.160"
    backup.vm.provider "virtualbox" do |v|
      config.vm.synced_folder ".", "/vagrant", disabled: true
      v.gui = false
      v.memory = 2048
      v.cpus = 2
    end
    backup.vm.disk :disk, name: "backup_storage", size: "2GB"
  end
  
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    #ansible.become = "true"
    ansible.limit = "all"
    ansible.host_key_checking = "false"
    ansible.inventory_path = "inventory/hosts"
  end  
end


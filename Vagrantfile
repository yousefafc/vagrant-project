# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'
guests = YAML.load_file("guest_machines.yml")
Vagrant.configure(2) do |config|
  guests.each do |guest|
    config.vm.define guest['name'] do |a1|
      a1.vm.box = guest['box']
      a1.vm.synced_folder ".", "/vagrant"
      a1.vm.network "private_network", ip: guest['private_ip']
	    
      a1.vm.provider "virtualbox" do |v|
        v.cpus = guest['cpus']
        v.memory = guest['memory']
        v.name = guest['name']
      end
      guest["script"].each do |script|
        a1.vm.provision "shell", path: script
      end
    end  
  end
end


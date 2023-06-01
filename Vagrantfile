# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2004"
  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"

  N = 4
  (1..N).each do |machine_id|
    config.vm.define "machine#{machine_id}" do |machine|
      machine.vm.hostname = "machine#{machine_id}"
      machine.vm.network "private_network", ip: "10.10.10.#{10+machine_id}"
      machine.vm.provider "virtualbox" do |vb|
        vb.memory = 1024
        vb.cpus = 1
      end

      if machine_id == N
        machine.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.inventory_path = "./inventory/hosts.yml"
          ansible.playbook = "master_playbook.yaml"
        end
      end
    end
  end
end

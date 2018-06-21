# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook           = "site.yml"
    ansible.compatibility_mode = "2.0"
    ansible.become             = true
    ansible.groups = {
      # "docker"              => ["default"],
      # "docker-swarm-master" => ["default"],
      "mysql"               => ["default"],
      # "nfs-client"          => ["default"],
    }
  end
end

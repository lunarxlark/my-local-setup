# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

#  if Vagrant.has_plugin?("vagrant-proxyconf")
#    config.proxy.http = "http://<proxy-ip>:<proxy-port>"
#    config.proxy.https = "http://<proxy-ip>:<proxy-port>"
#    config.proxy.no_proxy = "127.0.0.1,localhost"
#  end

  config.vm.box = "ubuntu/bionic64"
  config.vm.hostname = "bionic64"

  # config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.network "forwarded_port", guest: 443, host: 443
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "private_network", ip: "192.168.33.11"
  # config.vm.network "public_network"

  config.vm.synced_folder "../../../../../../src", "/home/vagrant/src", mount_optinos: ['dmode=777', 'fmode=755']

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "4096"
    vb.name = "bionic64"
    vb.cpus = 2
    vb.customize ['modifyvm', :id, "--ioapic", "on"]
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.provisioning_path  = "/vagrant"
    ansible.playbook           = "playbook.yml"
    ansible.inventory_path     = "inventory.ini"
    ansible.become             = true
    ansible.limit              = "all"
    ansible.install            = true
#    ansible.verbose            = true
    ansible.version            = "2.7.0"
    ansible.install_mode       = "pip"
    ansible.compatibility_mode = "2.0"
  end
end


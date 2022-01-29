# Defines our Vagrant environment
#
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # create some web servers
  # https://docs.vagrantup.com/v2/vagrantfile/tips.html
  (1..2).each do |i|
    config.vm.define "web#{i}" do |node|
        node.vm.box = "geerlingguy/centos7"
        node.vm.hostname = "web#{i}"
        node.vm.network :private_network, ip: "192.168.56.2#{i}"
        node.vm.network "forwarded_port", guest: 80, host: "808#{i}"
        node.vm.provider "virtualbox" do |vb|
          vb.memory = "512"
          vb.customize ['modifyvm', :id, '--memory', '2048']
          vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
          vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
        end
    end
  end

  # create load balancer
  config.vm.define :lb do |lb_config|
      lb_config.vm.box = "geerlingguy/centos7"
      lb_config.vm.hostname = "lb"
      lb_config.vm.network :private_network, ip: "192.168.56.11"
      lb_config.vm.network "forwarded_port", guest: 80, host: 8080
      lb_config.vm.provider "virtualbox" do |vb|
        vb.memory = "512"
        vb.customize ['modifyvm', :id, '--memory', '2048']
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      end
  end

  # create mgmt node
  config.vm.define :mgmt do |mgmt_config|
      mgmt_config.vm.box = "geerlingguy/centos7"
      mgmt_config.vm.hostname = "mgmt"
      mgmt_config.vm.network :private_network, ip: "192.168.56.10"
      mgmt_config.vm.provider "virtualbox" do |vb|
        vb.memory = "256"
        vb.customize ['modifyvm', :id, '--memory', '2048']
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      end
      mgmt_config.vm.provision :shell, path: "bootstrap-mgmt.sh"
  end

end

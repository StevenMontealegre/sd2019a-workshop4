# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false
  config.vm.define :load_balancer do |lb|
    lb.vm.box = "centos_7"
    lb.vm.network :private_network, ip: "192.168.56.101"
    lb.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "load_balancer" ]
    end
    lb.vm.provision "ansible" do |ansible|
      ansible.playbook = 'playbooks/lbplaybook.yml'
      ansible.inventory_path = 'inventory'
    end
  end
    
  config.vm.define :discovery_service do |ds|
    ds.vm.box = "centos_7"
    ds.vm.network :private_network, ip: "192.168.56.102"
    ds.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "consul_server" ]
    end    
    ds.vm.provision "ansible" do |ansible|
      ansible.playbook = 'playbooks/discovery_service.yml'
      ansible.inventory_path = 'inventory'
    end
  end

  config.vm.define :microservice_a do |ma|
    ma.vm.box = "centos_7"
    ma.vm.network :private_network, ip: "192.168.56.103"
    ma.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "microservice_a" ]
    end
    ma.vm.provision "ansible" do |ansible|
      ansible.playbook = 'playbooks/microservice_a.yml'
      ansible.inventory_path = 'inventory'
    end
  end
    
  config.vm.define :microservice_b do |mb|
    mb.vm.box = "centos_7"
    mb.vm.network :private_network, ip: "192.168.56.104"
    mb.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "1024","--cpus", "1", "--name", "microservice_b" ]
    end    
    mb.vm.provision "ansible" do |ansible|
      ansible.playbook = 'playbooks/microservice_b.yml'
      ansible.inventory_path = 'inventory'
    end
  end
    
end

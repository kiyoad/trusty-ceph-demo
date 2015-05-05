# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.define :sv1 do |conf|
    conf.vm.hostname = "sv1.local"
    conf.vm.network :private_network, ip: "10.0.0.51"
    conf.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", "1024" ]
    end
  end

  config.vm.define :sv2 do |conf|
    conf.vm.hostname = "sv2.local"
    conf.vm.network :private_network, ip: "10.0.0.52"
    conf.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", "1024" ]
    end
  end

  config.vm.define :sv3 do |conf|
    conf.vm.hostname = "sv3.local"
    conf.vm.network :private_network, ip: "10.0.0.53"
    conf.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", "1024" ]
    end
  end

  config.vm.define :deployer do |conf|
    conf.vm.hostname = "deployer.local"
    conf.vm.network :private_network, ip: "10.0.0.50"
    conf.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", "1024" ]
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/site.yml"
  end

end

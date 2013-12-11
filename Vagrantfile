# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
 
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :private_network, ip: "192.168.66.66"
  config.vm.hostname = 'caos-test.dev'
    
  config.vm.provider :virtualbox do |vb|
    vb.customize [
      "modifyvm", :id,
      "--memory", 1536,
      "--natdnshostresolver1", "on"
    ]
  end  
   
  config.vm.provision :chef_solo do |chef|   
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe "caos-test"

    chef.json = { 
      "apache" => {
        "listen_ports" => [ "80", "443" ]
      }
    }
  end

  # vagrant-omnibus (https://github.com/schisamo/vagrant-omnibus)
  config.omnibus.chef_version = :latest if Vagrant.has_plugin?("Omnibus")


  # vagrant-vbguest (https://github.com/dotless-de/vagrant-vbguest)
  config.vbguest.auto_update = true if Vagrant.has_plugin?("vbguest management")


  # vagrant-berkshelf (https://github.com/RiotGames/vagrant-berkshelf)
  config.berkshelf.enabled = false if Vagrant.has_plugin?("berkshelf")

end

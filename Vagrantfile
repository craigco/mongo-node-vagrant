Vagrant::Config.run do |config|
  config.vm.host_name = "fxdev-vagrant"
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.forward_port 3000, 80
  config.vm.network :bridged, "10.0.103.4"
  config.vm.share_folder "app", "/home/vagrant/app", "../", :nfs => false

  # allow for symlinks in the app folder
  config.vm.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/app", "1"]
  config.vm.customize ["modifyvm", :id, "--memory", 512]

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe "apt"
    chef.add_recipe "git"
    chef.add_recipe "php"
    chef.add_recipe "build-essential"
    chef.add_recipe "mongodb"
    chef.add_recipe "redis::server"
    chef.add_recipe "nodejs"
    chef.json = {
      "nodejs" => {
        "version" => "0.10.5",
        "from_source" => true
      }
    }
  end
end

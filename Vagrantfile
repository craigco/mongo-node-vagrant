Vagrant::Config.run do |config|
  config.vm.host_name = "fxdev-vagrant"
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.forward_port 3000, 3131
  config.vm.network :bridged, "10.0.103.33"
  config.vm.share_folder "app", "/opt/txtrproc/", "../src", :nfs => false

  # allow for symlinks in the app folder
  config.vm.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/app", "1"]
  config.vm.customize ["modifyvm", :id, "--memory", 1024]

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    chef.add_recipe "apt"
    chef.add_recipe "git"
    chef.add_recipe "php"
    chef.add_recipe "build-essential"
    chef.add_recipe "mongodb"
    chef.add_recipe "nodejs"
    chef.add_recipe "zeromq"
    chef.json = {
      "nodejs" => {
        "version" => "0.6.21",
        "from_source" => true
      }
    }
  end
end

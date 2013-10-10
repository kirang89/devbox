# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.synced_folder "./shared", "/shared"

  # Access the webserver in guest machine from the host using port forwarding
  config.vm.network :forwarded_port, guest: 8000, host: 8800

  config.vm.provider :virtualbox do |vb|
    # Uncomment this if you want to boot up into the gui of the vm
    # vb.gui = true

    # Specify the amount of memory to be used
    vb.customize ["modifyvm", :id, "--memory", "1024"]

    # Specify the number of CPU's to be used
    vb.customize ["modifyvm", :id, "--cpus", "2"]
  end

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"

    chef.add_recipe "apt"
    chef.add_recipe "sudo"
    chef.add_recipe "build-essential"
    chef.add_recipe "python"
    chef.add_recipe "vim"
    chef.add_recipe "git"
    chef.add_recipe "memcached"

    chef.json = {
      "authorization" => {
        'sudo' => {
          'agent_forwarding' => true,
          'users' => ["vagrant"],
          'passwordless' => true
        }
      }
    }
  end

  config.vm.provision :shell, :inline => "sudo apt-get install -y sqlite3"

  # Install necessary pip packages
  config.vm.provision :shell, :inline => "sudo pip install -r /shared/requirements.txt"

  # Add aliases to bashrc in the guest machine
  config.vm.provision :shell, :inline => "cat /shared/aliases.sh >> .bashrc"
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # more boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/trusty64"

  # Provision script that will upgrade the machine
  # config.vm.provision :shell, path: "bootstrap.sh"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-vagrantequired options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.post_up_message = "\n\n\n\n\n\n\n" + 
                              "This Box has these installed:"+
                              "\napache2" +
                              "\ngit" +
                              "\nNode.js +" + 
                              " npm\nJava 7 with JAVA_HOME and PATH set\n"

 

  # Use vagrant-omnibus plugin to install latest chef client
  config.omnibus.chef_version = :latest

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    # sudo apt-get install -y apache2
    # sudo apt-get install -y git
    sudo apt-get install -y locate

    # install node js and npm
    curl -sL https://deb.nodesource.com/setup | sudo bash -
    sudo apt-get install -y nodejs

    sudo knife cookbook site download java
    sudo mkdir -p /vagrant/cookbooks
    sudo tar xvzf java-*.tar.gz -C /vagrant/cookbooks

    # if ! [ -L /var/www ]; then
    #   rm -rf /var/www
    #   ln -fs /vagrant /var/www
    # fi

    # update locate db
    sudo updatedb
  SHELL


  config.vm.provision "chef_solo" do |chef|

    chef.cookbooks_path = ["cookbooks"]

    java_version = 7
    chef.json = { 
                  :java => { 
                    :install_flavor => "oracle",
                    :jdk_version => "7",
                    :set_etc_environment => true,
                    :oracle => {
                      :accept_oracle_download_terms => true
                    },
                    :jdk => {
                      :java_version =>  {
                        :x86_64 => {
                          :url => "http://download.oracle.com/otn-pub/java/jdk/7u75-b13/jdk-7u75-linux-x64.tar.gz",
                          :checksum => "6f1f81030a34f7a9c987f8b68a24d139"
                        }
                      }
                    }
                  }
                }

    chef.add_recipe "java"

  end

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true
  
    # Customize the amount of memory on the VM:
    # vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.

end

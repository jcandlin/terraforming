# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/focal64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

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
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "2048"
     vb.cpus = 2
   end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -qq
      sudo apt-get install -qq -y python3-pip unzip ruby apt-transport-https neofetch \
         ca-certificates curl software-properties-common docker.io ack-grep pkg-config \
         libusb-1.0-0 build-essential libpq-dev libssl-dev openssl libffi-dev zlib1g-dev \
         python3.8-dev git-flow bzip2 libsqlite3-dev libbz2-dev jq unzip dos2unix
      sudo systemctl enable --now docker
      sudo usermod -aG docker vagrant
      pip3 -q install boto3 pre-commit
      pip3 -q install --user pipenv
      git clone -q https://github.com/asdf-vm/asdf.git /home/vagrant/.asdf --branch v0.8.0
      rm /bin/sh
      ln -s /bin/bash /bin/sh
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      rm awscliv2.zip
      sudo ./aws/install
      rm -rf ./aws
      cat /vagrant/files/bashrc >> /home/vagrant/.bashrc
      mkdir /home/vagrant/.aws
      cp /vagrant/asdf/tool-versions /home/vagrant/.tool-versions
      cp /vagrant/asdf/asdfrc /home/vagrant/.asdfrc
      cp /vagrant/asdf/plugin.sh /home/vagrant/.asdf/plugin.sh
      dos2unix /home/vagrant/.asdf/plugin.sh
      dos2unix /home/vagrant/.tool-versions
      dos2unix /home/vagrant/.asdfrc
      cp /vagrant/aws/config /home/vagrant/.aws/
      chown -R vagrant. /home/vagrant/.asdf /home/vagrant/.tool-versions /home/vagrant/.asdfrc /home/vagrant/.aws
      su - vagrant -c "curl -sLf https://spacevim.org/install.sh | bash"
      su - vagrant -c "/home/vagrant/.asdf/plugin.sh > /tmp/asdf.log 2>&1"
      su - vagrant -c "source /home/vagrant/.asdf/asdf.sh;/home/vagrant/.asdf/bin/asdf install >> /tmp/asdf.log 2>&1"
      su - vagrant -c "/home/vagrant/.asdf/shims/starship init bash >> /home/vagrant/.bashrc"
   SHELL
end

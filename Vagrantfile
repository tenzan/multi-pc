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
  config.vm.box = "bento/ubuntu-20.04"

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
  config.vm.synced_folder "./data", "/vagrant"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true
    vb.cpus = "2"
  
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end

  config.vm.define "vb0" do |vb0|
    vb0.vm.hostname = "vb0"
    vb0.vm.network "private_network", ip: "10.20.30.100"
  end

  # config.vm.define "vb1" do |vb1|
  #     vb1.vm.hostname = "vb1"
  #     vb1.vm.network "private_network", ip: "10.20.30.101"
  # end

  # config.vm.define "vb2" do |vb2|
  #     vb2.vm.hostname = "vb2"
  #     vb2.vm.network "private_network", ip: "10.20.30.102"
  # end

  # config.vm.define "vb3" do |vb3|
  #   vb3.vm.hostname = "vb3"
  #   vb3.vm.network "private_network", ip: "10.20.30.103"
  # end

  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get update
    apt-get install -y python3-pip
    pip3 install apt-select
    # backup existing sources.list
    cp /etc/apt/sources.list{,.backup}
    # find best apt repository mirror
    apt-select --country JP
    mv sources.list /etc/apt/sources.list
    apt-get update
    apt-get install -y openvpn net-tools resolvconf
    cp /etc/netplan/01-netcfg.yaml /etc/netplan/01-netcfg.yaml.backup
    cp /vagrant/01-netcfg.yaml /etc/netplan/01-netcfg.yaml
    netplan apply
  SHELL
end

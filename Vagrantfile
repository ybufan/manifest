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
  config.vm.box = "bento/centos-8"

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
  
  # For Cockpit
  config.vm.network "forwarded_port", guest: 9090, host: 29090, host_ip: "127.0.0.1"
  
  # For SMTP
  config.vm.network "forwarded_port", guest: 25, host: 1025
  
  # For IMAP
  config.vm.network "forwarded_port", guest: 143, host: 1143

  # For POP3
  config.vm.network "forwarded_port", guest: 110, host: 1110

  # For submission
  config.vm.network "forwarded_port", guest: 587, host: 1587
  
  #for Apache
  config.vm.network "forwarded_port", guest: 80, host: 8080
  
  # dnsauth 
  config.vm.network "forwarded_port", guest: 54, host: 154, host_ip: "127.0.0.1"
  
  # dnsrecurs
  config.vm.network "forwarded_port", guest: 53, host: 153, host_ip: "127.0.0.1"

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
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = trueconfig.vm.provision "shell", path: "configure_mail_server.sh", run: 'always'
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "Package Installation", type: "shell", inline: <<-SHELL
     #Installation block
      config.vm.provision "puppet install", type: "shell", inline: <<-SHELL
    dnf -y install https://yum.puppetlabs.com/puppet-release-el-8.noarch.rpm
    yum -y install puppet
	yum -y install pdk
	  /opt/puppetlabs/bin/puppet module install puppet-archive
  SHELL
    
  config.vm.provision "puppet install pkgs", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "install_packages1.pp"
  end
  config.vm.provision "puppet roundcube install", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "install_rc2.pp"
  end
  config.vm.provision "puppet php-modules install", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "install_php3.pp"
  end
  config.vm.provision "puppet hostname change", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "change_hostname4.pp"
  end
  config.vm.provision "puppet mysql configuration", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "mysql_configure5.pp"
  end
  config.vm.provision "puppet creates Rouncube's config file", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "create_roundcube_conf_file6.pp"
  end
  config.vm.provision "puppet configures selinux files", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "selinux_configuration7.pp"
  end
  config.vm.provision "puppet creates php config file", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "create_php_conf_file8.pp"
  end
  config.vm.provision "puppet add users", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "add_users9.pp"
  end
  config.vm.provision "puppet config file modification", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "config_update10.pp"
  end
  config.vm.provision "puppet start and enable services", type: "puppet" do |puppet|
      puppet.manifests_path = "manifests"
      puppet.manifest_file = "services_starting11.pp"
  end
end

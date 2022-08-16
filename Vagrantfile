# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

#Script

#
$script =<<-SCRIPT
sudo yum -y update
sudo yum -y install wget
sudo yum -y install net-tools
sudo yum -y install tcpdump
sudo yum -y install nano

####-----To install ryslog------ ####
#cd /etc/yum.repos.d/
#sudo wget "http://rpms.adiscon.com/v8-stable-daily/rsyslog-daily.repo" # for CentOS 7
#sudo yum -y install rsyslog


####-----To install Syslog-ng------ ####
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -Uvh epel-release-latest-7.noarch.rpm
cd /etc/yum.repos.d/
wget https://copr.fedorainfracloud.org/coprs/czanik/syslog-ng336/repo/epel-7/czanik-syslog-ng335-epel-7.repo
sudo yum -y install syslog-ng
sudo systemctl enable syslog-ng
sudo systemctl start syslog-ng
SCRIPT
###End of Script ###

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: $script

end  
Vagrant.configure("2") do |config|
  if Vagrant.has_plugin?("vagrant-timezone")
    config.timezone.value = "Australia/Sydney"
  end

  config.vm.define "syslog-server" do | cfg|
    cfg.vm.box = "centos/7"
    cfg.vm.hostname = "syslog-server"
    cfg.vm.network :private_network, ip: "192.168.38.38"#, gateway: "192.168.38.1"
  end
  
  config.vm.define "test-server" do |cfg|
    cfg.vm.box   = "centos/7"
    cfg.vm.hostname = "test-server"
    cfg.vm.network :private_network, ip: "192.168.38.39"#, gateway: "192.168.38.1"
  end
  
  


end
#$ModLoad imudp
#$UDPServerRun 514

# Provides TCP syslog reception
#$ModLoad imtcp
#$InputTCPServerRun 514

##End of my notes



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
  #  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
   #  vb.memory = "4096"
  #end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
g

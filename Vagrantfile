# -*- mode: ruby -*-
# vi: set ft=ruby :

V_CPU = 1 # in cores
V_MEM = 512 # in megabytes per core
V_MEM_TOTAL = V_MEM * V_CPU
SYNC_TYPE = "rsync" # how to sync files in vagrant, for lxc rsync is suggested

$script = <<-SCRIPT
echo I am provisioning...
mkdir -p /home/vagrant/.ssh
cp -f /home/vagrant/ansible-from-zero/insecure_private_key /home/vagrant/.ssh/id_rsa
SCRIPT


VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # providers
  config.vm.provider "virtualbox" do |v|
    v.cpus = V_CPU
    v.memory = V_MEM_TOTAL
    v.customize ["modifyvm", :id, "--intnet3", "test"]
  end

  # virtual machines
  config.ssh.insert_key = false

  # control node
  config.vm.define "controller" do |s|
    s.vm.box = "generic/ubuntu1604"
    s.vm.network "private_network", ip: "192.168.50.7"
  end

  config.vm.define "centos" do |s|
    s.vm.box = "centos/7"
    s.vm.network "private_network", ip: "192.168.50.21"
    s.vm.network "private_network", auto_config: false, virtualbox__intnet: "test"
  end
  config.vm.define "debian" do |s|
    s.vm.box = "generic/debian9"
    s.vm.network "private_network", ip: "192.168.50.31"
    s.vm.network "private_network", auto_config: false, virtualbox__intnet: "test"
  end
  config.vm.define "ubuntu" do |s|
    s.vm.box = "generic/ubuntu1604"
    s.vm.network "private_network", ip: "192.168.50.11"
    s.vm.network "private_network", auto_config: false, virtualbox__intnet: "test"
  end


  ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
  config.vm.provision 'shell', inline: 'mkdir -p /root/.ssh'
  config.vm.provision 'shell', inline: "echo #{ssh_pub_key} >> /root/.ssh/authorized_keys"
  config.vm.provision 'shell', inline: "echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys", privileged: false
end
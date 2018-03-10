# -*- mode: ruby -*-
# vi: set ft=ruby :

box = 'ubuntu/trusty64'
repo = 'https://github.com/vnaboychenko/ansible_test.git'
$script = <<SCRIPT
apt-get install software-properties-common
apt-add-repository ppa:ansible/ansible
apt-get update
apt-get install git ansible -y
git clone "#{repo}"
chown vagrant:vagrant ansible_test/ -R
cat "/home/vagrant/.ssh/mykey" >> /home/vagrant/.ssh/authorized_keys
echo -n "[defaults]
host_key_checking = False
 " > ~vagrant/.ansible.cfg

SCRIPT

Vagrant.configure("2") do |config|
  config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/mykey"
  config.vm.provision "shell", inline: $script
  config.ssh.forward_agent = true
  config.vm.define "master" do |master|
    master.vm.box = box
    master.vm.hostname = 'master'

    master.vm.network :private_network, ip: "192.168.56.101"

box = 'ubuntu/trusty64'
    master.vm.provider :virtualbox do |v|
box = 'ubuntu/trusty64'
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "master"]
    end
  end

  config.vm.define "slave1" do |slave1|
    slave1.vm.box = box
    slave1.vm.hostname = 'slave1'

    slave1.vm.network :private_network, ip: "192.168.56.102"

    slave1.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "slave1"]
    end
  end

  config.vm.define "slave2" do |slave2|
    slave2.vm.box = box
    slave2.vm.hostname = 'slave2'

    slave2.vm.network :private_network, ip: "192.168.56.103"

    slave2.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "slave2"]
    end
  end

end

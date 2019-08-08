# -*- mode: ruby -*-
# vi: set ft=ruby :
#Provision ENV based on script
$script = <<-SCRIPT
#Install vulnerable docker runc
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce=17.03.0~ce-0~ubuntu-xenial
sudo usermod -aG docker vagrant
git clone https://github.com/dstubked/attacks.git
sudo apt-mark hold 4.4.0-21-generic
SCRIPT

Vagrant.configure("2") do |config|
N = 1
  # Specify your hostname if you like
(1..N).each do |machine_id|
  config.vm.box = "velocity42/xenial64"
  config.vm.box_check_update = false
  config.vm.define "pg-0#{machine_id}" do |machine|
    machine.vm.hostname = "pg-0#{machine_id}"
    machine.vm.network "private_network", type: "dhcp"
  config.vm.provision "shell", inline: $script
  config.vm.provider "virtualbox" do |v|
    v.cpus = 1
    v.memory = 2048
  end
end
end
end

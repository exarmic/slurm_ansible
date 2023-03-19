# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

#  config.vm.provision "file", source: "files/gitlab_slurm_rsa.pub", destination: "/home/vagrant/.ssh/"

  config.vm.define "server_centos_ansible" do |server_centos|
    server_centos.vm.box = "centos-7.9"
    server_centos.vm.hostname = "centos"
    server_centos.vbguest.auto_update = false
    server_centos.vm.network "private_network", ip: "192.168.56.83"
    server_centos.vm.synced_folder "./","/home/vagrant/ansible" 
    server_centos.vm.provision "shell", inline: <<-SHELL
      sudo yum install -y epel-release
      sudo yum install -y ansible git
      git clone https://github.com/exarmic/slurm_ansible.git
    SHELL
  end


end

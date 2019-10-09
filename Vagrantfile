# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "bento/ubuntu-18.04"
  
  config.disksize.size = '25GB'
  
  config.ssh.forward_x11 = true

  config.vm.network "private_network", ip: "192.168.50.4"
  config.vm.network :forwarded_port, guest: 8080, host: 8080

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
  end
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/debian11"
  config.vm.synced_folder "./", "/mnt/vagrant", type: "sshfs"

  config.vm.provider "libvirt" do |v|
    v.memory = 512
    v.cpus = 2
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.skip_tags = "vagrant"
  end
end

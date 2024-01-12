# -*- mode: ruby -*-
# vi: set ft=ruby :

VM_PROVIDER = "virtualbox"

# Master server config
MASTER_ENABLED = 1
MASTER_COUNT = 1
MASTER_CPU = 2
MASTER_MEMORY = 768
MASTER_BOX = "generic/debian12"
PORTS = [80, 443]

# Backup server config
BACKUP_ENABLED = 0
BACKUP_COUNT = 2
BACKUP_CPU = 1
BACKUP_MEMORY = 384
BACKUP_BOX = "generic/debian12"


Vagrant.configure("2") do |config|
  # Master nodes
  if MASTER_ENABLED == 1
    (1..MASTER_COUNT).each do |i|
      PORTS.each do |port|
        config.vm.network "forwarded_port", guest: port, host: port
      end

      config.vm.define "master_#{i}" do |machine|
        machine.vm.box = MASTER_BOX
        machine.vm.synced_folder "./", "/mnt/vagrant"
        machine.vm.network "private_network", ip: "192.168.66.#{10 + i}"

        machine.vm.provider VM_PROVIDER do |v|
          v.cpus = MASTER_CPU
          v.memory = MASTER_MEMORY
        end
      end
    end
  end

  # Backup nodes
  if BACKUP_ENABLED == 1
    (1..BACKUP_COUNT).each do |i|
      config.vm.define "backup_#{i}" do |machine|
        machine.vm.box = BACKUP_BOX
        machine.vm.synced_folder "./", "/mnt/vagrant"
        machine.vm.network "private_network", ip: "192.168.66.#{127 + i}"

        machine.vm.provider VM_PROVIDER do |v|
          v.cpus = BACKUP_CPU
          v.memory = BACKUP_MEMORY
        end
      end
    end
  end
end

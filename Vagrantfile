# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "stakahashi/amazonlinux2"
  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  config.vm.provider :virtualbox do |v|
      v.name = "al2lepp"
      v.memory = 4096
      v.cpus = 2
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    config.vm.synced_folder "shared", "/var/www", type: "nfs",
        mount_options: ['rw', 'vers=3', 'tcp', 'fsc'],
        linux__nfs_options: ['rw','no_subtree_check','all_squash','async']

    config.vm.synced_folder ".", "/vagrant", type: "nfs",
        mount_options: ['rw', 'vers=3', 'tcp', 'fsc'],
        linux__nfs_options: ['rw','no_subtree_check','all_squash','async']

    config.vm.hostname = "al2lepp"
    config.vm.network :private_network, ip: "10.200.200.201"

    # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
    config.vm.define :al2lepp do |al2lepp|

    end

    # Ansible provisioner.
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/playbook.yml"
        ansible.become = true
    end

    if Vagrant.has_plugin?("vagrant-reload")
        config.vm.provision :reload
    end
end

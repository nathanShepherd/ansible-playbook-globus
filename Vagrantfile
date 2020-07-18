# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.ssh.insert_key = true

  config.vm.box = "centos/7"

  config.vm.define "globus-server" do |box|
    box.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = 1024
    end
    box.vm.network "private_network", ip: "10.1.1.11"
    box.vm.hostname = "globus-server"
  end

  config.vm.define "globus-client" do |box|
    box.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = 1024
    end
    box.vm.network "private_network", ip: "10.1.1.12"
    box.vm.hostname = "globus-client"

    box.vm.provision "ansible" do |ansible|
      ansible.playbook = "site.yml"
      ansible.limit = "all"

      ansible.groups = {
        "globus-servers" => ["globus-server"],
        "globus-clients" => ["globus-client"]
      }

      ansible.sudo = true
      # ansible.ask_vault_pass = true
      # ansible.vault_password_file = "vault_pass_file"
      # ansible.tags = ""
      # ansible.skip_tags = ""
      # ansible.verbose = "vv"
    end
  end
end

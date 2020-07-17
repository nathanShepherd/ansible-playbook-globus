# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.ssh.insert_key = true

  config.vm.box = "centos/7"

  config.vm.define "gridftp-server.local" do |box|
    box.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = 1024
    end
    box.vm.network "private_network", ip: "10.1.1.1"
    box.vm.hostname = "globus_server"
  end

  config.vm.define "gridftp-client.local" do |box|
    box.vm.provider "virtualbox" do |vb|
        vb.cpus = 2
        vb.memory = 1024
    end
    box.vm.network "private_network", ip: "10.1.1.2"
    box.vm.hostname = "globus_client"

    box.vm.provision "ansible" do |ansible|
      ansible.playbook = "site.yml"
      ansible.limit = "all"

      ansible.groups = {
        "globus_servers" => ["globus_server"],
        "globus_clients" => ["globus_client"]
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

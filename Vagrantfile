# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.network "public_network"

  config.vm.provision "ansible" do |ansible|
    ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
    ansible.groups = {
      "ldap" => ["ldap1", "ldap2"],
      "sftp" => ["sftp"],
      "web" => ["web"],
      "all_groups:children" => ["ldap", "sftp", "web"]
    }
    ansible.playbook = "provisioning/playbook.yml"
  end

  config.vm.define "ldap1" do |ldap1|
    ldap1.vm.box = "chef/centos-6.5"
    ldap1.vm.hostname = "ldap1.local"
    ldap1.vm.network :public_network, ip: "192.168.24.100"
  end

  config.vm.define "ldap2" do |ldap2|
    ldap2.vm.box = "chef/centos-6.5"
    ldap2.vm.hostname = "ldap2.local"
    ldap2.vm.network :public_network, ip: "192.168.24.101"
  end

  config.vm.define "sftp" do |sftp|
    sftp.vm.box = "chef/centos-6.5"
    sftp.vm.hostname = "sftp.local"
    sftp.vm.network :public_network, ip: "192.168.24.102"
  end

  config.vm.define "web" do |web|
    web.vm.box = "chef/centos-6.5"
    web.vm.hostname = "web.local"
    web.vm.network :public_network, ip: "192.168.24.103"
  end

end

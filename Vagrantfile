# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = "https://atlas.hashicorp.com/ubuntu/trusty64"

  config.vm.define "nansat", primary: true do |course|
    course.vm.network :private_network, ip: "192.168.33.10"
  end

  config.vm.define "course", autostart: false do |develop|
    develop.vm.network :private_network, ip: "192.168.33.11"
  end

  config.vm.define "catalog", autostart: false do |catalog|
    catalog.vm.network :private_network, ip: "192.168.33.12"
  end

  config.vm.define "doppler", autostart: false do |catalog|
    catalog.vm.network :private_network, ip: "192.168.33.13"
  end

  config.vm.provider "virtualbox" do |v|
    v.memory = 4000
    v.cpus = 2
  end

  # If true, then any SSH connections made will enable agent forwarding.
  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provisioning/site.yml"
    ansible.inventory_path = "provisioning/hosts"
    ansible.provisioning_path = "/vagrant"
    ansible.verbose = "vvv"
    ansible.install = true
    ansible.install_mode = "pip"
  end

end

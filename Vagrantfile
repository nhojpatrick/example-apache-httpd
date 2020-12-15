# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # default box
  config.vm.box = "centos/7"

  # do not auto upgrade on boot
  config.vm.box_check_update = false
  config.vbguest.auto_update = false
  config.vbguest.no_remote = true

  # setup custom ssh keys
  config.ssh.insert_key = false
  config.ssh.private_key_path = [
    'provisioning/.ssh/id_rsa',
    '~/.vagrant.d/insecure_private_key'
  ]
  config.vm.provision 'file', 
    source: 'provisioning/.ssh/id_rsa.pub', 
    destination: '~/.ssh/authorized_keys'
  config.vm.provision 'file',
    source: 'provisioning/.ssh/id_rsa',
    destination: '~/.ssh/id_rsa'

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.cpus = "1"
    vb.memory = "512"
    vb.customize ["modifyvm", :id, "--audio", "none"]
  end

  config.vm.define "touchdown", autostart: false do |inst|
    # ubuntu 20.04 Focal Fossa 2020-04 - eol 2025-04
    inst.vm.box = "ubuntu/focal64"
    inst.vm.boot_timeout = 1200
    inst.vm.hostname = "touchdown"
    inst.vm.network "private_network", ip: "192.168.123.199"
    inst.vm.synced_folder ".", "/vagrant"

    # automated ansible install fails so manual install
    inst.vm.provision "shell", inline: "sudo apt update"
    inst.vm.provision "shell", inline: "sudo apt install -y ansible"
  end

  config.vm.define "webhost0", autostart: true do |inst|
    inst.vm.box = "centos/7"
    inst.vm.hostname = "webhost0"
    inst.vm.network "private_network", ip: "192.168.123.190"
    inst.vm.network :forwarded_port, guest: 22, host: 2290
    inst.vm.network :forwarded_port, guest: 8080, host: 8180
  end

  config.vm.define "webhost1", autostart: true do |inst|
    inst.vm.box = "centos/7"
    inst.vm.hostname = "webhost1"
    inst.vm.network "private_network", ip: "192.168.123.191"
    inst.vm.network :forwarded_port, guest: 22, host: 2291
    inst.vm.network :forwarded_port, guest: 8080, host: 8181
  end

  config.vm.define "webhost2", autostart: true do |inst|
    inst.vm.box = "centos/7"
    inst.vm.hostname = "webhost2"
    inst.vm.network "private_network", ip: "192.168.123.192"
    inst.vm.network :forwarded_port, guest: 22, host: 2292
    inst.vm.network :forwarded_port, guest: 8080, host: 8182
  end

end

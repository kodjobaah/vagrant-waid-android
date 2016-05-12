# -*- mode: ruby -*-
# vi: set ft=ruby :
# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  #config.vm.provision :shell, :path => 'bootstrap.sh'
  config.vm.provision :ansible do |ansible|
     ansible.playbook = "playbook.yml"
  end
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "appium-ansible"

  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "5048"
    # Customize the number  of CPUs allocated
    vb.cpus = 1
    # If you want more than one CPU you must enable I/O APIC
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional", "--vram", "256", "--accelerate3d", "on"]
    vb.customize ['modifyvm', :id, '--usb', 'on']
    vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant", "1"]
    vb.customize ['usbfilter', 'add', '0', '--target', :id, '--name', 'Galaxy Nexus', '--vendorid', '0x04e8']
  end
end

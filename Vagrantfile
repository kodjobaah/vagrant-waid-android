box      = 'phusion/ubuntu-14.04-amd64'
version  = 2

Vagrant.configure(version) do |config|
    config.vm.box = box

    # Now let puppet do its thing.
    config.vm.provision :puppet do |puppet|
      puppet.manifests_path = 'puppet/manifests'
      puppet.manifest_file = 'devenv.pp'
      puppet.module_path = 'puppet/modules'
      puppet.options = "--verbose"
    end
    

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
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
  end

  # Start Xorg on boot
 # Install xfce and virtualbox additions
  config.vm.provision "shell", inline: "sudo apt-get update"
  config.vm.provision "shell", inline: "sudo apt-get install -y xfce4 virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11"
  # Permit anyone to start the GUI
  config.vm.provision "shell", inline: "sudo sed -i 's/allowed_users=.*$/allowed_users=anybody/' /etc/X11/Xwrapper.config"

  config.vm.provision "shell", inline: "sudo systemctl set-default graphical.target && sudo systemctl isolate graphical.target"
end

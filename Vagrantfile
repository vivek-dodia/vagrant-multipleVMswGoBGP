Vagrant.configure("2") do |config|
  # VM names
  vm_names = ["CR1", "CR2", "ER1", "ER2"]

  # Iterate over VM names to define each VM
  vm_names.each do |name|
    config.vm.define name do |machine|
      machine.vm.box = 'ubuntu/focal64'
      machine.vm.hostname = name
      machine.vm.provider "virtualbox" do |vb|
        vb.name = name
        vb.cpus = 4
        vb.memory = '4096'
      end

      # Provisioning block to install packages
      machine.vm.provision "shell", inline: <<-SHELL
        # Update the system
        sudo apt-get update

        # Install necessary tools
        sudo apt-get install -y traceroute nano gobgpd net-tools

        # Add Go binaries to the PATH
        echo 'export PATH=$PATH:$HOME/go/bin' >> ~/.profile
        source ~/.profile
      SHELL
    end
  end
end

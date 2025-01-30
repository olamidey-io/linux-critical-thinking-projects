Vagrant.configure("2") do |config|
  # Define the bastion server
  config.vm.define "bastion" do |bastion|
    bastion.vm.box = "ubuntu/focal64"
    bastion.vm.box_version = "20240821.0.1"  # Specify version
    bastion.vm.network "private_network", ip: "192.168.34.10"
    bastion.vm.hostname = "bastion"
    # Port forward for SSH access
    bastion.vm.network "forwarded_port", guest: 22, host: 2220, id: "ssh"
    bastion.vm.synced_folder ".", "/vagrant", disabled: true  # Disable synced folder if not needed
    bastion.vm.provider "virtualbox" do |vb|
      vb.memory = 512
      vb.name = "bastion.server"
    end
  end
  # Define the other servers
  (1..3).each do |i|
    config.vm.define "server#{i}" do |server|
      server.vm.box = "ubuntu/focal64"
      server.vm.box_version = "20240821.0.1"  # Specify version
      server.vm.network "private_network", ip: "192.168.34.1#{i}"
      server.vm.hostname = "server#{i}"
      server.vm.provider "virtualbox" do |vb|
        vb.memory = 512
        vb.name = "server#{i}_vm"
      end
    end
  end
end
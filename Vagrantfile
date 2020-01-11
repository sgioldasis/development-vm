# -*- mode: ruby -*-
# vi: set ft=ruby :
class VagrantPlugins::ProviderVirtualBox::Action::Network
  def dhcp_server_matches_config?(dhcp_server, config)
    true
  end
end

require 'yaml'
settings = YAML.load_file 'vagrant.yml'

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  # Define node_name 
  node_name = settings['vm_name']

  # Define node_number 
  node_number = 1

  # Private network required for nfs synced folder
  config.vm.network "private_network", type: "dhcp"
    
  # # Share folder
  # config.vm.synced_folder "./shared", "/home/vagrant/shared"
  config.vm.synced_folder ".", "/vagrant"

  # Provisioner
  provisioner = Vagrant::Util::Platform.windows? ? :guest_ansible : :ansible

  # Define settings for each node
  config.vm.define node_name do |node|

    # Every Vagrant development environment requires a box. You can search for
    # boxes at https://vagrantcloud.com/search.
    node.vm.box = settings['vm_box']

    # Determine node_ip based on the configured vm_ip_prefix 
    # node_ip = settings['vm_ip_prefix']+"."+"#{node_number+10}"

    # Create a private network, which allows access to the machine using node_ip
    # node.vm.network "private_network", ip: node_ip
    # node.vm.network "public_network"

    # Private_netword required for nfs synced folder
    # node.vm.network "private_network", type: "dhcp"

    # Share folder
    # node.vm.synced_folder "./shared", "/home/vagrant/shared"

    # Provider-specific configuration so you can fine-tune various
    # backing providers for Vagrant. These expose provider-specific options.
    # Below configuration targets VirtualBox:
    node.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = settings['vm_gui']
    
      # Customize the amount of memory on the VM:
      vb.memory = settings['vm_memory']

      # Customize the name of the VM:
      vb.name = node_name

      # Customize the settings of the VM:
      vb.customize ["modifyvm", :id, "--vram", "128"]
      vb.customize ["modifyvm", :id, "--graphicscontroller", "VMSVGA"]
      vb.customize ["modifyvm", :id, "--accelerate3d", "on"]
      vb.customize ["modifyvm", :id, "--hwvirtex", "on"]
      vb.customize ["modifyvm", :id, "--nestedpaging", "on"]
      vb.customize ["modifyvm", :id, "--accelerate2dvideo", "off"]
      # vb.customize ["modifyvm", :id, '--audio', 'pulse']
      vb.customize ["modifyvm", :id, '--audiocontroller', 'ac97']
      vb.customize ["modifyvm", :id, "--audioin", "on"]
      vb.customize ["modifyvm", :id, "--audioout", "on"]

    end
    
    # Ansible provisioning

    # Disable the new default behavior introduced in Vagrant 1.7, to
    # ensure that all Vagrant machines will use the same SSH key pair.
    # See https://github.com/mitchellh/vagrant/issues/5005
    node.ssh.insert_key = false

    # Call Ansible also passing it values needed for configuration
    # node.vm.provision "ansible" do |ansible|
    node.vm.provision provisioner do |ansible|
      ansible.verbose = "v"
      ansible.playbook = "playbook.yml"
    #   ansible.extra_vars = {
    #     node_ip_address: node_ip,
    # }
    end

  end
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
HOST_NAME = BOX_NAME = "hugobox"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|


  config.vm.box = BOX_NAME
  config.vm.hostname = HOST_NAME
  config.vm.box_url = "http://wavelength.se/arch-basebox/arch-base.box"

  config.ssh.forward_agent = true

  # IP network configuration.
  #config.vm.network :private_network, ip: "192.33.33.25"

  # Shared folders.
  config.vm.synced_folder "data", "/home/vagrant/data", create: true, id: "vagrant-root",
    owner: "vagrant",
    group: "vagrant",
    mount_options: ["dmode=775,fmode=764"]

  # Provider-specific VM configuration.
  config.vm.provider :virtualbox do |v|
    v.name = HOST_NAME
    v.customize ["modifyvm", :id, "--memory", 512]
    # vb.customize ["modifyvm", :id, "--cpus", "2"]
    # vb.gui = true
  end

  # Anible provisionning.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.extra_vars = {
      ansible_python_interpreter: "/usr/bin/python2"
    }
    # If something goes wrong, you'll want Ansible to be more verbose.
    # ansible.verbose = true
  end

end

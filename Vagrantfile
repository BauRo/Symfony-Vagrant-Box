##
# Vagrant box for Symfony projects
# Made by BauRo (roy@bauweraerts.com)
##

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.ssh.insert_key = true

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.define "dev-server" do |web|
    web.vm.network "private_network", ip: "192.168.5.115",
        auto_config: true
    web.vm.network "public_network", bridge: 'en0: Wi-Fi (AirPort)'
  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = ""
    ansible.playbook = "ansible/dev.yml"
    ansible.limit = "dev-server"
    ansible.extra_vars = { vagrantserver: true }
  end

end

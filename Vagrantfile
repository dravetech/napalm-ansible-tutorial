# -*- mode: ruby -*-
# vi: set ft=ruby :
"""
You will need the boxes:

 * vEOS-4.17.5M
 * JunOS - juniper/ffp-12.1X47-D20.7-packetmode
    * To provision and test JunOS first you have to add the ssh vagrant ssh key into the ssh-agent. I.e.:
		ssh-add /opt/vagrant/embedded/gems/gems/vagrant-`vagrant --version | awk '{ print $2 }'`/keys/vagrant
 * csr100v - ask your Cisco sales rep (sic)
"""

Vagrant.configure(2) do |config|
  config.vbguest.auto_update = false

  config.vm.define "eos" do |eos|
    eos.vm.box = "vEOS-lab-4.17.5M"

    eos.vm.network :forwarded_port, guest: 443, host: 12443, id: 'https'

    eos.vm.network "private_network", virtualbox__intnet: "link_1", ip: "169.254.1.11", auto_config: false
    eos.vm.network "private_network", virtualbox__intnet: "link_2", ip: "169.254.1.11", auto_config: false
  end

  config.vm.define "ios" do |ios|
    ios.vm.box = "csr1000v"

    ios.vm.network :forwarded_port, guest: 22, host: 12202, id: 'ssh'

    ios.vm.network "private_network", virtualbox__intnet: "link_1", ip: "169.254.1.11", auto_config: false
    ios.vm.network "private_network", virtualbox__intnet: "link_2", ip: "169.254.1.11", auto_config: false
  end

  config.vm.define "junos" do |junos|
    junos.vm.box = "juniper/ffp-12.1X47-D20.7-packetmode"

    junos.vm.network :forwarded_port, guest: 22, host: 12203, id: 'ssh'

    junos.vm.network "private_network", virtualbox__intnet: "link_1", ip: "169.254.1.11", auto_config: false
    junos.vm.network "private_network", virtualbox__intnet: "link_2", ip: "169.254.1.11", auto_config: false
  end

end

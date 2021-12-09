# -*- mode: ruby -*-
# vi: set ft=ruby :
#!/usr/bin/env ruby


image = "debian/buster64"

vms = {
 'gitlab-ce' => {'memory' => '4096', 'cpus' => '1', 'ip' => '10', 'box' => "#{image}"},
}

Vagrant.configure('2') do |config|
  vms.each do |name, conf|
     config.vm.define "#{name}" do |my|
       my.vm.box = conf['box']
       my.vm.hostname = "#{name}.example.com"
       my.vm.network 'private_network', ip: "192.168.59.#{conf['ip']}"
       my.vm.provider 'virtualbox' do |vb|
          vb.memory = conf['memory']
          vb.gui = false
          vb.name = "#{name}"
          vb.cpus = conf['cpus']
          vb.customize ["modifyvm", :id, "--usb", "off"]
          vb.customize ["modifyvm", :id, "--usbehci", "off"]
       end
       my.vm.provision "ansible" do |ansible|
         ansible.playbook = "playbook.yml"
       end
     end
  end
end



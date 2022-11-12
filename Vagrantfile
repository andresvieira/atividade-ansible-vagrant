# -*- mode: ruby -*-
# vi: set ft=ruby :

vms = {
    'wordpress' => {'memory' => '2048', 'cpus' => 1, 'ip' => '50', 'box' => 'bento/ubuntu-18.04', 'provision' => 'provisionamento/install-wordpress.yml'}
  }
  
  Vagrant.configure('2') do |config|
  
    config.vm.box_check_update = false
  
          if !(File.exists?('id_rsa'))
            system("ssh-keygen -b 2048 -t rsa -f id_rsa -q -N ''")
         end
  
    vms.each do |name, conf|
      config.vm.define "#{name}" do |k|
        k.vm.box = "#{conf['box']}"
        k.vm.hostname = "#{name}.labs"
        k.vm.network 'private_network', ip: "192.168.56.#{conf['ip']}"
        k.vm.provider 'virtualbox' do |vb|
          vb.customize ["modifyvm", :id, "--groups", "/Ansible"]
          vb.name = conf["name"]
          vb.memory = conf['memory']
          vb.cpus = conf['cpus']
          
        end
        k.vm.provision 'ansible_local' do |ansible|
          ansible.playbook = "#{conf['provision']}"
        end
    end
    end
  end
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Virtual hosts used for Devoxx presentation
  hosts = {
            :app1 => { :name => "app1", :address => "10.10.2.20" }, # application server #1
            :app2 => { :name => "app2", :address => "10.10.2.21" }  # application server #2
          }

  # Host setup template
  hosts.each do |host, params|
    config.vm.define "#{ params[:name] }" do |host|
      host.vm.box = "Centos-6.5-minimal-x86_64-20140116"
      host.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"

      host.vm.provider :virtualbox do |vb|
        vb.customize [
                         "modifyvm", :id,
                         "--name", "devoxx-sample-#{ params[:name] }",
                         "--memory", 512,
                         "--cpus", 1,
                     ]
      end
      host.vm.network :private_network, ip: "#{ params[:address] }"
      host.vm.hostname = "#{ params[:name] }.devoxx-sample"
      host.vm.provision "shell", inline: "sudo yum -y install python-httplib2" # Required to use 'uri' Ansible module
    end
  end
end

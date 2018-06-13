Vagrant.configure("2") do |config|

  config.vm.provision "shell", inline: <<-SHELL
      echo "172.25.1.10 server.example.com smtp.example.com web.example.com server" >> /etc/hosts
      echo "172.25.1.11 desktop.example.com desktop" >> /etc/hosts
  SHELL

  config.vm.define "server" do |instance|
    instance.vm.box = "centos/7"
    instance.vm.hostname = 'server'
    instance.vm.synced_folder '.', '/vagrant', disabled: true
    instance.vm.network :private_network, ip: "172.17.0.10"
    instance.vm.network :private_network, type: "dhcp", auto_config: false
    instance.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "server"]

      serverDisk1 = './serverDisk1.vdi'

      if not File.exists?(serverDisk1)
        v.customize ['createhd', '--filename', serverDisk1, '--variant', 'Standard', '--size', 2 * 1024]
      end
      v.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 1, '--type', 'hdd', '--medium', serverDisk1]
    end
  end

  config.vm.define "desktop" do |instance|
    instance.vm.box = "centos/7"
    instance.vm.hostname = 'desktop'
    instance.vm.synced_folder '.', '/vagrant', disabled: true
    instance.vm.network :private_network, ip: "172.17.0.11"
    instance.vm.network :private_network, type: "dhcp", auto_config: false

    instance.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "desktop"]
    end
  end
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :php do |php_config|
    php_config.vm.box = "precise32"
    php_config.vm.box_url = "http://files.vagrantup.com/precise32.box"

    php_config.ssh.forward_agent = true

    php_config.vm.network "public_network", {:bridge => 'Broadcom NetLink (TM) Gigabit Ethernet'}
    php_config.vm.network :forwarded_port, guest: 80, host: 1080
    php_config.vm.network :forwarded_port, guest: 443, host: 1443

    php_config.vm.hostname = "g2k-php"

    php_config.vm.synced_folder "C:\\WebsitesPHP", "/var/www", {:mount_options => ['dmode=777', 'fmode=777']}
    php_config.vm.provision :shell, :inline => "echo \"Europe/Rome\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

    php_config.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", "512"]
    end

    php_config.vm.provision :shell, :inline => "sudo apt-get update"
    php_config.vm.provision :shell, :inline => "sudo apt-get install -y curl lftp"
    php_config.vm.provision :shell, :inline => "curl -sL https://raw2.github.com/Graffiti2000Srl/easyengine/master/install.sh | sudo bash && sudo ee system install"
  end
end

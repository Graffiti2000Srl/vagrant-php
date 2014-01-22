# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :php do |php_config|
    php_config.vm.box = "precise32"
    php_config.vm.box_url = "http://files.vagrantup.com/precise32.box"

    php_config.ssh.forward_agent = true

    php_config.vm.network :forwarded_port, guest: 80, host: 1080
    php_config.vm.network :forwarded_port, guest: 443, host: 1443

    php_config.vm.hostname = "g2k-php"

    php_config.vm.synced_folder "C:\\WebsitesPHP", "/var/www", {:mount_options => ['dmode=777', 'fmode=777']}
    php_config.vm.provision :shell, :inline => "echo \"Europe/Rome\" | sudo tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata"

    php_config.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", "512"]
    end

    php_config.vm.provision :shell, :inline => "sudo apt-get updatel"
    php_config.vm.provision :shell, :inline => "sudo apt-get install -y curl"
    php_config.vm.provision :shell, :inline => "curl -sL rt.cx/ee | sudo bash && sudo ee system install"
  end
end

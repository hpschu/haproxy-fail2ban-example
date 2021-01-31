# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "generic/debian10"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"


  config.vm.synced_folder "./configs", "/vagrant_data"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y haproxy fail2ban openssh-server
    apt-get install -y apache2
    cp /vagrant_data/haproxy.cfg /etc/haproxy/haproxy.cfg
    cp /vagrant_data/ports.conf /etc/apache2/ports.conf
    cp /vagrant_data/000-default.conf /etc/apache2/sites-available/000-default.conf
    cp /vagrant_data/4xx-filter.conf /etc/fail2ban/filter.d/4xx-filter.conf
    cp /vagrant_data/4xx-jail.conf /etc/fail2ban/jail.d/4xx-jail.conf
    service apache2 restart
    service haproxy restart
    service rsyslog restart
  SHELL
end

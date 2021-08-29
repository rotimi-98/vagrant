# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "app" do |app|
    app.vm.synced_folder "app/", "/var/www/app",
      create: true, group: "vagrant", owner: "vagrant", id: "app"
    app.vm.network "forwarded_port", guest: 8080, host: 8081,
    auto_correct: true, id: "wanderer-app"
    app.vm.network "private_network", type: "dhcp"
  end
  config.vm.define "prom" do |prom|
    prom.vm.network "forwarded_port", guest:9090, host:9090,
      auto_correct: true, id: "prometheus"
    prom.vm.network "private_network", type: "dhcp"
  end
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

# $script = <<-SCRIPT
# apt-get install nodejs npm
# SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.define "app" do |app|
    app.vm.hostname = "app"
    app.vm.synced_folder "app/", "/var/www/app",
      create: true, group: "vagrant", owner: "vagrant", id: "app"
    app.vm.network "forwarded_port", guest: 8080, host: 8081,
    auto_correct: true, id: "wanderer-app"
    app.vm.network "private_network", type: "dhcp"
#   app.vm.provision "shell", inline: "apt-get install -y nodejs npm"
#   app.vm.provision "shell", inline: $script
    app.vm.provision "shell", path: "scripts/pre.sh"
    app.vm.provision "file", source: "configs/services", destination: "/tmp/services"
    app.vm.provision "shell", path: "scripts/post.sh"
  end

  config.vm.define "prom" do |prom|
    prom.vm.hostname = "prom"
    prom.vm.network "forwarded_port", guest:9090, host:9090,
      auto_correct: true, id: "prometheus"
    prom.vm.network "private_network", type: "dhcp"
  end
end

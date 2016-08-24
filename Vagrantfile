# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/trusty64"

  # Make the default GoCD port available on the local host
  config.vm.network "forwarded_port", guest: 8153, host: 8153

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end

  config.vm.provision "shell", inline: <<-SHELL

    # Add GoCD official
    echo "deb https://download.go.cd /" | sudo tee /etc/apt/sources.list.d/gocd.list
    curl https://download.go.cd/GOCD-GPG-KEY.asc | sudo apt-key add -
    apt-get update

    apt-get install -y openjdk-7-jre-headless git
    apt-get install -y go-server
    apt-get install -y go-agent

    apt-get autoremove -y

    # the go agent doesn't start automatically - might as well make sure the server is running
    service go-server start
    service go-agent start

  SHELL

end

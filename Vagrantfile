# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
  "vm01" => { "memory" => "1024", "cpu" => "2", "ip" => "101", "image" => "ubuntu/bionic64" },
  "vm02" => { "memory" => "1024", "cpu" => "2", "ip" => "102", "image" => "ubuntu/bionic64" },
  "vm03" => { "memory" => "1024", "cpu" => "2", "ip" => "103", "image" => "ubuntu/bionic64" }
}

Vagrant.configure("2") do |config|
  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}.healthcheck"
      machine.vm.network "private_network", ip: "10.20.20.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.customize ["modifyvm", :id, "--groups", "/Healthcheck"]
      end
      machine.vm.provision "shell", path: "provision.sh"
      machine.vm.provision "shell", inline: "hostnamectl set-hostname #{name}.healthcheck"
    end
  end
end
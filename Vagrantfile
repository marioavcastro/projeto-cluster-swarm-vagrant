# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
  "master" => {"memory" => "512", "cpu" => "1", "ip" => "100", "image" => "ubuntu/focal64"},
  "node01" => {"memory" => "512", "cpu" => "1", "ip" => "101", "image" => "ubuntu/focal64"},
  "node02" => {"memory" => "512", "cpu" => "1", "ip" => "102", "image" => "ubuntu/focal64"},
  "node03" => {"memory" => "512", "cpu" => "1", "ip" => "102", "image" => "ubuntu/focal64"}
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "192.168.56.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.customize ["modifyvm", :id, "--groups", "/Docker-Lab"]
      end
      machine.vm.provision "shell", path: "docker.sh"
      if "#{name}" == "master"
        machine.vm.provision "shell", path: "master.sh"
      else
        machine.vm.provision "shell", path: "worker.sh"
      end
    end
  end
end

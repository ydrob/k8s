NUM_WORKER_NODES=2
NUM_MASTER_NODES=3
IP_NW="172.21.0."

Vagrant.configure("2") do |config|
    config.vm.provision "shell", inline: <<-SHELL
        apt-get update -y
        echo "172.21.0.2  master-1.local" >> /etc/hosts
		echo "172.21.0.3  master-2.local" >> /etc/hosts
		echo "172.21.0.4  master-3.local" >> /etc/hosts
		echo "172.21.0.5  ingress-1.local" >> /etc/hosts
        echo "172.21.0.6  node-1.local" >> /etc/hosts
		echo "172.21.0.7  node-2.local" >> /etc/hosts
    SHELL
    config.vm.box = "bento/ubuntu-20.04"
    config.vm.box_check_update = true


    (1..NUM_WORKER_NODES).each do |i|
      config.vm.define "node-#{i}.local" do |node|
        node.vm.hostname = "node-#{i}.local"
        node.vm.network "private_network", ip: IP_NW + "#{5 + i}"
        node.vm.provider "virtualbox" do |vb|
            vb.memory = 2048
            vb.cpus = 1
            vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        end
      end
    end

    config.vm.define "ingress" do |ingress|
      ingress.vm.hostname = "ingress-1.local"
      ingress.vm.network "private_network", ip: "172.21.0.5"
      ingress.vm.provider "virtualbox" do |vb|
          vb.memory = 2048
          vb.cpus = 1
          vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      end
    end



    (1..NUM_MASTER_NODES).each do |i|
      config.vm.define "master-#{i}.local" do |node|
        node.vm.hostname = "master-#{i}.local"
        node.vm.network "private_network", ip: IP_NW + "#{1 + i}"
        node.vm.provider "virtualbox" do |vb|
            vb.memory = 2048
            vb.cpus = 1
            vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        end
      end
    end
  end
  

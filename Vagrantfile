IMAGE_NAME = "alvistack/ubuntu-22.04"
N = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
        v.cpus = 2
    end

	config.vm.synced_folder "./vm_share", "/vm_share"

    config.vm.define "master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "master"
    end

    (1..N).each do |i|
        config.vm.define "worker-#{i}" do |worker|
            worker.vm.box = IMAGE_NAME
            worker.vm.network "private_network", ip: "192.168.50.#{i + 10}"
            worker.vm.hostname = "worker-#{i}"
        end
    end

	config.vm.provision "apt update and upgrade", type: "shell", inline: <<-SHELL
		sudo apt update -y
		sudo apt upgrade -y
	SHELL
end

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.boot_timeout = 1200
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  #configure provisioners on tha machine
  config.vm.provision :docker
  config.vm.provision :docker_compose

  config.vm.define "server-1" do |server1|
   server1.vm.network "private_network", ip: '192.168.33.61'
   server1.vm.hostname = "server-1"
   server1.vm.provision "shell", path: "provision.sh"
  end

  config.vm.define "server-2" do |server2|
    server2.vm.network "private_network", ip: '192.168.33.62'
    server2.vm.hostname = "server-2"
  end

end
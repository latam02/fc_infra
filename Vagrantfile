$script = <<-SCRIPT
echo "I like Vagrant"
echo "I love Linux"
date > /home/vagrant/vagrant_provisioned_at
SCRIPT


Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.boot_timeout = 1200
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  #configure provisioners on tha machine
  config.vm.provision :docker
  config.vm.provision :docker_compose
  config.vm.provision :shell, path: "./scripts/bootstrap.sh"
  config.vm.provision :file, source: "Prueba", destination:"folder"

  config.vm.define "server-1" do |server1|
   server1.vm.network "private_network", ip: '192.168.33.61'
   server1.vm.hostname = "server-1"
   server1.vm.provision "shell", path: "provision.sh"
  end

  config.vm.define "server-2" do |server2|
    server2.vm.network "private_network", ip: '192.168.33.62'
    server2.vm.hostname = "server-2"
    server2.vm.provision "shell", inline: "echo Hi Class!"
    server2.vm.provision "shell", inline: $script
    server2.vm.provision "shell" do |s|
      s.inline = "echo $1"
      s.args = ["AT", "Class!"]
    end

    server2.vm.provision "docker" do |d|
      d.run "hello-world"
    end

  end

end
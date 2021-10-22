Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.boot_timeout = 1200
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  #configure provisioners on tha machine
  config.vm.provision :docker
  config.vm.provision :docker_compose

  config.vm.define "ci-server" do |ci_server|
    ci_server.vm.network "private_network", ip: '192.168.33.61'
    ci_server.vm.hostname = "ci-server"
    ci_server.vm.provision :file, source:"./docker/docker-compose.ci.yml", destination:"/home/vagrant/docker-compose.yml"
    ci_server.vm.provision :docker_compose, yml:"/home/vagrant/docker-compose.yml", run:"always"
  end

  config.vm.define "server-2" do |server2|
    server2.vm.network "private_network", ip: '192.168.33.62'
    server2.vm.hostname = "server-2"
    server2.vm.provision :docker_compose, yml: "/vagrant/MachineLearning/docker-compose.yml", rebuild: true, run: "always"
  end

end

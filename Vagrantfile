Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.boot_timeout = 1200
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "6144"
    vb.cpus = "4"
  end

  #configure provisioners on tha machine
  config.vm.provision :docker
  config.vm.provision :docker_compose

  config.vm.define "ci-server" do |ci_server|
    ci_server.vm.network "private_network", ip: '192.168.33.61'
    ci_server.vm.hostname = "ci-server"
    ci_server.vm.provision :file, source:"./docker/docker-compose.ci.yml", destination:"/home/vagrant/docker-compose.yml"
    ci_server.vm.provision :docker_compose, yml:"/home/vagrant/docker-compose.yml", run:"always"
    ci_server.vm.provision :shell, inline: "sudo chmod 777 /var/run/docker.sock"
  end

  config.vm.define "cd-server" do |cd_server|
    cd_server.vm.network "private_network", ip: '192.168.33.62'
    cd_server.vm.hostname = "cd-server"
    cd_server.vm.provision :file, source:"./docker/docker-compose.cd.yml", destination:"/home/vagrant/docker-compose.yml"
    cd_server.vm.provision :docker_compose, yml:"/home/vagrant/docker-compose.yml", run:"always"
    cd_server.vm.provision :shell, inline: "sudo chmod 777 /var/run/docker.sock"
  end

end

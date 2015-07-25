# -*- mode: ruby -*-
# vi: set ft=ruby :
$setupDocker = <<SCRIPT
# Stop and remove any existing containers
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)

# Build containers from Dockerfiles


# Run and link the containers


SCRIPT

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
#Check if you have the good Vagrant version to use docker provider...
Vagrant.require_version ">= 1.6.0"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.define "ubuntu", autostart: true
    config.vm.define "centos", autostart: false
    config.vm.synced_folder "../", "/usr/share/nginx/html/www", \
      :create         => true, \
      :owner          => 'vagrant', \
      :group          => 'vagrant', \
      :mount_options  => ['dmode=777,fmode=777']

    # Ubuntu box
    config.vm.define "ubuntu" do |web|
        web.vm.box = "ubuntu/trusty64"
        web.vm.network :private_network, ip: "192.168.33.33"
        web.vm.provision "shell", path: "scripts/config.sh"
        web.vm.provision "shell", path: "scripts/ubuntu/base.sh"
        web.vm.provision "shell", path: "scripts/ubuntu/mysql.sh"
        web.vm.provision "shell", path: "scripts/ubuntu/nginx.sh"
        web.vm.provision "shell", path: "scripts/ubuntu/php.sh"
        web.vm.provision "shell", path: "scripts/ubuntu/phalcon.sh"
        web.vm.provision "shell", path: "scripts/app.sh"

    end

    config.vm.define "centos" do |web|
        web.vm.box = "centos/7"
        web.vm.network :private_network, ip: "192.168.33.33"
        web.vm.provision "shell", path: "scripts/centos/base.sh"
        web.vm.provision "shell", path: "scripts/config.sh"
        #web.vm.provision "shell", path: "scripts/centos/mysql.sh"
        #web.vm.provision "shell", path: "scripts/centos/php.sh"
        web.vm.provision "shell", path: "scripts/centos/nginx.sh"
        #web.vm.provision "shell", path: "scripts/centos/phalcon.sh"
    end

end

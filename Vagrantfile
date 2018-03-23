Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_check_update = false
  config.vm.synced_folder "shared/", "/shared", create: true
  config.vm.synced_folder "dataset/", "/dataset", create: true

# forward ports used for created NodeJS websites
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 8000, host: 8000

# forward port for MongoDB (in case we need to use Compass to connect to it)
  config.vm.network "forwarded_port", guest: 27017, host: 27017

  config.vm.define "mongod-m101js" do |server|
    server.vm.provider "virtualbox" do |vb|
	     vb.customize ["modifyvm", :id, "--cpus", "2"]
       vb.name = "mongod-m101js"
       vb.memory = 2048
    end
    server.vm.hostname = "m101js.mongodb.university"
    server.vm.network :private_network, ip: "192.168.103.100"
    server.vm.provision :shell, path: "provision-mongod", args: ENV['ARGS']
    server.vm.provision :shell, path: "provision-node", args: ENV['ARGS'], privileged: false
  end
end

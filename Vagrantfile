$prepare = <<SCRIPT
# sudo apt-get update
curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
apt-get install git gzip git curl python libssl-dev pkg-config build-essential nodejs redis-server -y
#windows vagrant hack
mkdir /home/vagrant/node_modules
chown vagrant:vagrant /home/vagrant/node_modules
ln -sf /home/vagrant/node_modules /vagrant/src/node_modules
chown vagrant:vagrant /vagrant/src/node_modules
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 9001, host: 8888
  config.vm.provision "shell", inline: $prepare

  # Forward des connexions ssh
  config.ssh.forward_agent = true

  config.vm.provider "virtualbox" do |v|
    v.name   = "etherpad-lite"
    v.memory = 2048
  end
end

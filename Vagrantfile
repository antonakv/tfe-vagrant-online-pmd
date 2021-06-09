Vagrant.configure("2") do |config|
  config.vm.box = "aakulov/bionic64"
  config.vm.hostname = "ptfeinteractive"
  config.vm.network "private_network", ip: "192.168.56.33"

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024 * 4
    v.cpus = 2
    v.name = "tfe-vagrant-online-pmd"
  end
  config.vm.provision "shell", path: "scripts/mountdisk.sh"
end

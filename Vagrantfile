$script = <<SCRIPT
rpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
yum -y install libselinux-python
yum -y install ansible python-setuptools
yum -y update gmp
SCRIPT


Vagrant.configure("2") do |config|
  config.vm.box = "chef/centos-6.6"

  config.vm.network "forwarded_port", guest: 4567, host: 14567
  config.vm.network "forwarded_port", guest: 5555, host: 15555
  config.vm.network "forwarded_port", guest: 5556, host: 15556

  config.vm.provision "shell", inline: $script

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning.yml"
  end

  # config.vm.provision :docker do |d|
  #   d.pull_images "centos:centos6"
  # end
  # config.vm.provision :shell, path: "setup.sh"
  # config.vm.provision :shell, path: "runpacker.sh", privileged: false
  config.vm.provider "virtualbox" do |v|
    v.memory = 1536
  end
end

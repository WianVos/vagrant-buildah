# -*- mode: ruby -*-
# vi: set ft=ruby :
## Provisioning script
$script = <<SCRIPT
  mkdir ~/buildah
  cd ~/buildah
  export GOPATH=`pwd`
  git clone https://github.com/projectatomic/buildah ./src/github.com/projectatomic/buildah
  cd ./src/github.com/projectatomic/buildah
  make
  sudo make install
  buildah --help
SCRIPT

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure("2") do |config|
  config.vm.box = "fedora/26-cloud-base"
  config.vm.box_version = "20170705"
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end
  config.vm.provision "shell",
    inline: "dnf -y install make golang bats btrfs-progs-devel device-mapper-devel glib2-devel gpgme-devel libassuan-devel ostree-devel git bzip2 go-md2man runc skopeo-containers"
  config.vm.provision "shell", inline: $script, privileged: false
end
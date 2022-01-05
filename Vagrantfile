# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "archlinux/archlinux"

  config.vm.provision "shell", inline: <<-SHELL
    pacman --noconfirm -Syu docker
    pacman -U /vagrant/crun/crun-1.4-1-x86_64.pkg.tar.zst
    mkdir -p /etc/docker
    curl -o /etc/docker/daemon.json \
      https://gist.githubusercontent.com/BlackIkeEagle/ff1d11edad999627f1a2eaf86b0d508e/raw/7ace97c045ccacdd9267e3feb08b03193ce0d761/daemon.json
    systemctl enable docker.service
    systemctl reboot
  SHELL
end

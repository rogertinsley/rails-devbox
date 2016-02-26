# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box      = "ubuntu/trusty64"
  config.vm.hostname = "rails-dev"
  config.vm.network :forwarded_port, guest: 3000, host: 3000

  config.vm.provision "shell", inline: <<-SHELL

    # system
    sudo apt-get update
    sudo apt-get install libgmp-dev --yes

    # Node
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

    # RVM
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
    curl -sSL https://get.rvm.io | bash -s stable
    source /usr/local/rvm/scripts/rvm

    # Ruby
    rvm use 2.3.0 --install --default

    # Gem
    gem update --system
    echo "gem: --no-ri --no-rdoc" > ~/.gemrc
    gem install bundler

    # Rails
    gem install rails -v 4.2.4

    # Postgres
    sudo apt-get install postgresql libpq-dev --yes
    sudo -u postgres createuser -s vagrant

    # Git
    sudo apt-get install git --yes

    # GitHub Hub
    wget https://github.com/github/hub/releases/download/v2.2.3/hub-linux-amd64-2.2.3.tgz
    tar xvf hub-linux-amd64-2.2.3.tgz
    cd hub-linux-amd64-2.2.3
    chmod +x install
    sudo ./install
    rm -rf hub-linux-amd64-2.2.3*

    # Vagrant Permissions
    sudo chown -R vagrant /usr/local/rvm

  SHELL
end

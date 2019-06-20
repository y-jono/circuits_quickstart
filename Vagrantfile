# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/bionic64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder ".", "/host"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
    #sudo apt-get update
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    sudo apt-get install -y picocom
    sudo apt-get install -y build-essential automake autoconf git squashfs-tools ssh-askpass
    sudo apt-get install -y git libssl-dev libncurses5-dev \
        bc m4 make unzip cmake python autoconf \
        libwxgtk3.0-dev libgl1-mesa-dev libglu1-mesa-dev \
        libglfw3 libglfw3-dev libglew2.0 libglew-dev
    curl -L -O https://github.com/fhunleth/fwup/releases/download/v1.3.1/fwup_1.3.1_amd64.deb -o fwup_1.3.1_amd64.deb
    if [ ! -d "$HOME/.asdf" ]; then
        git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.7.2
        echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.bashrc
        echo -e '\n. $HOME/.asdf/completions/asdf.bash' >> ~/.bashrc # optional
    fi
    source ~/.bashrc
    sudo apt-get install libwxgtk3.0-dev
    if hash erl 2>/dev/null; then
        echo "erl installed."
    else
        asdf plugin-add erlang
        asdf install erlang 21.3.6
        asdf global erlang 21.3.6
    fi
    if hash elixir 2>/dev/null; then
        echo "elixir installed."
    else
        asdf plugin-add elixir
        asdf install elixir 1.8.1-otp-21
        asdf global elixir 1.8.1-otp-21
    fi
  SHELL
end


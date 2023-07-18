VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.hostname = "ansible.local"
    config.vm.provider "virtualbox" do |vb|
        vb.memory = 1024
    end

    if Vagrant.has_plugin?("vagrant-vbguest")
        config.vbguest.auto_update = false
    end

    config.vm.network "private_network", ip: "192.168.56.46"
    config.vm.synced_folder ".", "/vagrant", type: "rsync", rsync__exclude: [".git/"]

    config.vm.provision "shell", inline: <<-SHELL
        export DEBIAN_FRONTED=noninteractive
        sudo apt -y update
        sudo apt install -y ca-certificates apt-transport-https
        sudo apt install -y software-preperties-common curl
        sudo apt install -y python3-pip python-is-python3
        sudo add-apt-repository --yes --update ppa:ansible/ansible
        sudo apt install -y ansible
        sudo pip3 install docker
    SHELL
end
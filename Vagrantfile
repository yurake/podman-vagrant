Vagrant.configure("2") do |config|
  config.vm.box = "bento/fedora-30"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.33.30"
  config.vm.hostname = "fedora-30-podman-mac-client"
  config.vm.define "fedora-30-podman-mac-client"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "fedora-30-podman-mac-client"
    vb.cpus = 2
    vb.memory = 4096
  end

  config.vm.provision :hosts do |provisioner|
    provisioner.autoconfigure = true
    provisioner.add_host '192.168.64.19', ['default-route-openshift-image-registry.apps-crc.testing']
  end

  config.vm.provision "shell", inline: <<-SHELL
    ## install podman ##
    sudo yum -y install podman git
    ## install custom image settings ##
    git clone https://github.com/yurake/k8s-3tier-webapp.git
  SHELL
end


Vagrant.configure("2") do |config|
  config.vm.define "node01" do |master|
    master.vm.box = "bento/ubuntu-22.04"
    master.vm.hostname = "master-node.klno01"
    config.ssh.username = "vagrant"
    config.ssh.password = "vagrant"
    master.vm.network "private_network", ip: "192.168.56.85"
    master.vm.synced_folder ".", '/home/vagrant/'
    master.vm.provider "virtualbox" do |vb|
      vb.name = "master-node01"
      vb.cpus = 4
      vb.memory = 8192
      vb.gui = false
    end
    config.vm.provision "shell", run: "always", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install net-tools zip curl jq tree unzip wget siege apt-transport-https ca-certificates software-properties-common gnupg lsb-release -y
      netstat -tunlp
      echo "Hello from hellocloud-native-box"
    SHELL

    config.vm.provision "shell",
      privileged: true,
      path: './scripts/docker_install.sh'

    config.vm.provision "shell",
      privileged: true,
      path: './scripts/kube_install.sh'

    config.vm.provision "shell",
      privileged: true,
      path: './scripts/kind_install.sh'

    config.vm.provision "shell",
      privileged: true,
      path: './scripts/helm.sh'

    config.vm.provision "shell",
      privileged: true,
      path: './scripts/grpcurl.sh'
  end
end
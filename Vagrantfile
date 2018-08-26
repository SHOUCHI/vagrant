Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.disksize.size = '50GB'

  #centos
  config.vm.define "centos" do |centos|
    centos.vm.network "forwarded_port", guest: 22, host: 2242, host_ip: "127.0.0.1", id: "ssh", auto_correct: true
    centos.vm.network "private_network", ip: "192.168.56.13"
    centos.vm.hostname = "centos"

    centos.vm.provider "virtualbox" do |vb|
      vb.memory = "1048"
      vb.cpus = 1
    end
  end  
end

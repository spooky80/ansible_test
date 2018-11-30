BOX_IMAGE = "centos/7"
NODE_COUNT = 2


Vagrant.configure("2") do |config|
  config.vm.define "master" do |subconfig|
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "master"
    subconfig.vm.network :forwarded_port, guest: 80,  host: 8080,  id: :http,  auto_correct: true # HTTP
    subconfig.vm.network :forwarded_port, guest: 443, host: 9443, id: :https, auto_correct: true # HTTPS
  end

  config.vm.define "oldMaster" do |subconfig|
    subconfig.vm.box = "centos/7"
    subconfig.vm.box_version = "1804.02"
    subconfig.vm.hostname = "oldMaster"
    subconfig.vm.network :forwarded_port, guest: 80,  host: 9090,  id: :http,  auto_correct: true # HTTP
    subconfig.vm.network :forwarded_port, guest: 443, host: 4443, id: :https, auto_correct: true # HTTPS
  end
  
  (1..NODE_COUNT).each do |i|
    config.vm.define "node#{i}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "node#{i}"
      config.vm.usable_port_range = 8000..8999
      subconfig.vm.network :forwarded_port, guest: 80,  host: 8080,  id: :http,  auto_correct: true # HTTP
    subconfig.vm.network :forwarded_port, guest: 443, host: 9443, id: :https, auto_correct: true # HTTPS
    end
end
config.vm.provision "ansible" do |ansible|
ansible.playbook = "site.yml"
end
end

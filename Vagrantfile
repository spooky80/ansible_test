Vagrant.configure("2") do |config|

  config.vm.box = "centos/7"
  config.vm.box_version = "1809.01"
  config.vbguest.auto_update = false
 
  config.vm.define "db" do |db|
    db.vm.network "private_network", ip: "192.168.50.20"
    db.vm.hostname = "dbhost"
  end

  config.vm.define "web" do |web|
    web.vm.network "forwarded_port", guest: 80, host: 8080
    web.vm.network "private_network", ip: "192.168.50.10"
    web.vm.hostname = "webhost"
  end
 
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "site.yml"
     ansible.groups = {
       "webservers" => ["web"],
       "dbservers" => ["db"]
     }
  end
 
 end
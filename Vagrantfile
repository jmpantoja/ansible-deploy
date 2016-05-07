Vagrant.require_version ">= 1.5"
Vagrant.configure("2") do |config|

  config.vm.define "redmine", autostart: false do |redmine|
    redmine.vm.provider :virtualbox do |v|
        v.name = "redmine"
        v.customize [
            "modifyvm", :id,
            "--name", "redmine",
            "--memory", 512,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end  
 
    redmine.vm.box = "debian/jessie64"
    redmine.vm.box_check_update = true
    redmine.vm.hostname = "redmine"
    
    redmine.vm.network "private_network", ip: "192.168.50.10"
    redmine.vm.network "public_network", use_dhcp_assigned_default_route: true
	
    redmine.vm.synced_folder ".", "/vagrant", type: "nfs"
    redmine.vm.synced_folder "/deploy", "/deploy", type: "nfs", mount_options: ['rw', 'vers=3', 'tcp', 'fsc' ,'actimeo=2']

    redmine.vm.provision "ansible" do |ansible|
	  ansible.sudo = true
      ansible.playbook = "ansible/playbook.yml"
      ansible.inventory_path = "./ansible/inventory"
      ansible.limit = "redmine"
    end
  end
  

  config.vm.define "monitoring", autostart: false do |monitoring|

    monitoring.vm.provider :virtualbox do |v|
        v.name = "monitoring"
        v.customize [
            "modifyvm", :id,
            "--name", "monitoring",
            "--memory", 1024,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end  
 
    monitoring.vm.box = "ubuntu/trusty64"
    monitoring.vm.box_check_update = true
    monitoring.vm.hostname = "monitoring"
    
    monitoring.vm.network "private_network", ip: "192.168.50.20"
    monitoring.vm.network "public_network", use_dhcp_assigned_default_route: true
	
    monitoring.vm.synced_folder ".", "/vagrant", type: "nfs"
    monitoring.vm.synced_folder "/deploy", "/deploy", type: "nfs", mount_options: ['rw', 'vers=3', 'tcp', 'fsc' ,'actimeo=2']

    monitoring.vm.provision "ansible" do |ansible|
	  ansible.sudo = true
      ansible.playbook = "ansible/playbook.yml"
      ansible.inventory_path = "./ansible/inventory"
      ansible.limit = "monitoring"
    end
  end  

  config.vm.define "web", autostart: false do |web|

    web.vm.provider :virtualbox do |v|
        v.name = "web"
        v.customize [
            "modifyvm", :id,
            "--name", "web",
            "--memory", 512,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end  
 
    web.vm.box = "ubuntu/trusty64"
    web.vm.box_check_update = true
    web.vm.hostname = "web"
    
    web.vm.network "private_network", ip: "192.168.50.59"
    web.vm.network "public_network", use_dhcp_assigned_default_route: true
	
    web.vm.synced_folder ".", "/vagrant", type: "nfs"
    web.vm.synced_folder "/deploy", "/deploy", type: "nfs", mount_options: ['rw', 'vers=3', 'tcp', 'fsc' ,'actimeo=2']

    web.vm.provision "ansible" do |ansible|
	  ansible.sudo = true
      ansible.playbook = "ansible/playbook.yml"
      ansible.inventory_path = "./ansible/inventory"
      ansible.limit = "web"
    end
  end  
  
end

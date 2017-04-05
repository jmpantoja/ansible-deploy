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

  config.vm.define "website", autostart: false do |website|

    website.vm.provider :virtualbox do |v|
        v.name = "website"
        v.customize [
            "modifyvm", :id,
            "--name", "website",
            "--memory", 1024,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end  
 
    website.vm.box = "ubuntu/trusty64"
    website.vm.box_check_update = true
    website.vm.hostname = "website"
    
    website.vm.network "private_network", ip: "192.168.50.50"
    website.vm.network "public_network", use_dhcp_assigned_default_route: true
	
    website.vm.synced_folder ".", "/vagrant", type: "nfs"
    website.vm.synced_folder "/deploy", "/deploy", type: "nfs", mount_options: ['rw', 'vers=3', 'tcp', 'fsc' ,'actimeo=2']

    website.vm.provision "ansible" do |ansible|
	  ansible.sudo = true
      ansible.playbook = "ansible/playbook.yml"
      ansible.inventory_path = "./ansible/inventory"
      ansible.limit = "website"
    end
  end  
  
  config.vm.define "replica", autostart: false do |replica|

    replica.vm.provider :virtualbox do |v|
        v.name = "replica"
        v.customize [
            "modifyvm", :id,
            "--name", "replica",
            "--memory", 1024,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end  
 
    replica.vm.box = "ubuntu/trusty64"
    replica.vm.box_check_update = true
    replica.vm.hostname = "replica"
    
    replica.vm.network "private_network", ip: "192.168.50.60"
    replica.vm.network "public_network", use_dhcp_assigned_default_route: true
	
    replica.vm.synced_folder ".", "/vagrant", type: "nfs"
    replica.vm.synced_folder "/deploy", "/deploy", type: "nfs", mount_options: ['rw', 'vers=3', 'tcp', 'fsc' ,'actimeo=2']

    replica.vm.provision "ansible" do |ansible|
	  ansible.sudo = true
      ansible.playbook = "ansible/playbook.yml"
      ansible.inventory_path = "./ansible/inventory"
      ansible.limit = "replica"
    end
  end    
  
end

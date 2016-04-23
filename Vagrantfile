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
  

  config.vm.define "storage", autostart: false do |storage|
    storage.vm.provider :virtualbox do |v|
        v.name = "storage"
        v.customize [
            "modifyvm", :id,
            "--name", "storage",
            "--memory", 512,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end  
 
    storage.vm.box = "debian/jessie64"
    storage.vm.box_check_update = true
    storage.vm.hostname = "storage"
    
    storage.vm.network "private_network", ip: "192.168.50.20"
    storage.vm.network "public_network", use_dhcp_assigned_default_route: true
	
    storage.vm.synced_folder ".", "/vagrant", type: "nfs"
    storage.vm.synced_folder "/CODE", "/CODE", type: "nfs", mount_options: ['rw', 'vers=3', 'tcp', 'fsc' ,'actimeo=2']

    storage.vm.provision "ansible" do |ansible|
	  ansible.sudo = true
      ansible.playbook = "ansible/playbook.yml"
      ansible.inventory_path = "./ansible/inventory"
      ansible.limit = "storage"
    end
  end  
  
end

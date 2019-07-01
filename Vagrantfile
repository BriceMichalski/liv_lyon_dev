
require 'yaml'

# Read YAML file with box details
settings = YAML.load_file('settings.yml')

Vagrant.configure('2') do |config|

	#basic settings
	config.vm.define settings['vm_name']
	config.vm.box = settings['vm_box']

	####################
	# VM Configuration #
	####################
	config.vm.provider "virtualbox" do |v|
  		v.name = settings['vm_name']
		v.gui = false
    		v.customize ["modifyvm", :id, "--ioapic", "on"]
    		v.customize [ "modifyvm", :id, "--cpus", settings["proc"] ]
    		v.customize [ "modifyvm", :id, "--memory", settings["ram"] ]
	end

	#################
	#   Network 	#
	#################
	# Default HTTP port
	config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
	# MySQL port
  	config.vm.network "forwarded_port", guest: 3306, host: 3307, auto_correct: true

	#################
	# Synced folder #
	#################
	config.vm.synced_folder "./", "/vagrant", id: "vagrant-root"

	if settings["synced"]
	    settings["synced"]["folders"].each do |sf_name, sf|
	        config.vm.synced_folder sf["host_path"], sf["guest_path"]
	    end
	end

	#################
	# Provisionning #
	#################
	config.vm.provision "platform", type:"ansible_local" do |ansible|
	  ansible.galaxy_role_file = '/vagrant/provisionning/ansible/requirements.yml'
	  ansible.playbook = "/vagrant/provisionning/ansible/build_liv_lyon_platform.yml"
	  ansible.inventory_path = "/vagrant/provisionning/ansible/environment/DEV/DEV"
	  ansible.limit = "all"
	end

	config.vm.provision "app", type:"ansible_local" do |ansible|
    	    ansible.playbook = "/vagrant/provisionning/ansible/deploy_app.yml"
	    ansible.inventory_path = "/vagrant/provisionning/ansible/environment/DEV/DEV"
	    ansible.limit = "all"
	end
end

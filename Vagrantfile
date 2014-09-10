# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
config.vm.box = "centos-65-x64-nocm"
config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-65-x64-virtualbox-nocm.box"

pe_version = '3.3.0'
config.pe_build.version       = pe_version
config.pe_build.download_root = "https://s3.amazonaws.com/pe-builds/released/#{pe_version}"

## Master
config.vm.define :master do |master|

master.vm.provider :virtualbox do |v|
v.memory  = 1024
v.cpus = 2
end

master.vm.network :private_network,  ip: "10.10.100.100"
master.vm.network "forwarded_port", guest: 443, host: 8443
master.vm.hostname = 'master.puppetlabs.vm'
master.vm.provision :hosts

master.vm.provision :pe_bootstrap do |pe|
pe.role = :master
end

config.vm.provision "shell", 
	inline: "service iptables stop"
	end

## Production 
	config.vm.define :production do |prod|

	prod.vm.provider :virtualbox
	prod.vm.network :private_network,  ip: "10.10.100.111"

	prod.vm.hostname = 'production.puppetlabs.vm'
	prod.vm.provision :hosts

	prod.vm.provision :pe_bootstrap do |pe|
	pe.role   =  :agent
	pe.master = 'master.puppetlabs.vm'
	end
	end

## Development
	config.vm.define :development do |dev|

	dev.vm.provider :virtualbox
	dev.vm.network :private_network,  ip: "10.10.100.112"

	dev.vm.hostname = 'development.puppetlabs.vm'
	dev.vm.provision :hosts

	dev.vm.provision :pe_bootstrap do |pe|
	pe.role   =  :agent
	pe.master = 'master.puppetlabs.vm'
	end
	end

## Testing 
	config.vm.define :testing do |test|

	test.vm.provider :virtualbox
	test.vm.network :private_network,  ip: "10.10.100.113"

	test.vm.hostname = 'testing.puppetlabs.vm'
	test.vm.provision :hosts

	test.vm.provision :pe_bootstrap do |pe|
	pe.role   =  :agent
	pe.master = 'master.puppetlabs.vm'
	end
	end
## Registry/Git
	config.vm.define :gitreg do |gr|

	gr.vm.provider :virtualbox
	gr.vm.network :private_network,  ip: "10.10.100.114"

	gr.vm.hostname = 'testing.puppetlabs.vm'
	gr.vm.provision :hosts

	gr.vm.provision :pe_bootstrap do |pe|
	pe.role   =  :agent
	pe.master = 'master.puppetlabs.vm'
	end
	end
	end

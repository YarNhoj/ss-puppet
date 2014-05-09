# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
config.vm.box = "centos-65-x64-nocm"
config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-65-x64-virtualbox-nocm.box"

pe_version = '3.2.2'
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

## agent 1
	config.vm.define :agent1 do |agent|

	agent.vm.provider :virtualbox
	agent.vm.network :private_network,  ip: "10.10.100.111"

	agent.vm.hostname = 'agent1.puppetlabs.vm'
	agent.vm.provision :hosts

	agent.vm.provision :pe_bootstrap do |pe|
	pe.role   =  :agent
	pe.master = 'master.puppetlabs.vm'
	end
	end

## agent 2
	config.vm.define :agent2 do |agent|

	agent.vm.provider :virtualbox
	agent.vm.network :private_network,  ip: "10.10.100.112"

	agent.vm.hostname = 'agent2.puppetlabs.vm'
	agent.vm.provision :hosts

	agent.vm.provision :pe_bootstrap do |pe|
	pe.role   =  :agent
	pe.master = 'master.puppetlabs.vm'
	end
	end

## agent 3
	config.vm.define :agent3 do |agent|

	agent.vm.provider :virtualbox
	agent.vm.network :private_network,  ip: "10.10.100.113"

	agent.vm.hostname = 'agent3.puppetlabs.vm'
	agent.vm.provision :hosts

	agent.vm.provision :pe_bootstrap do |pe|
	pe.role   =  :agent
	pe.master = 'master.puppetlabs.vm'
	end
	end
	end

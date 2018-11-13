# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'                                              #load yml package
guests = YAML.load_file("guest_machines.yml")               #define 'guests' according to the yml file
Vagrant.configure(2) do |config|                            #initialize config file
  guests.each do |guest|		                    #'guests' was defined above when loading yml file, 'guest' will run guests.each since we need to do each guest
    config.vm.define guest['name'] do |guest_vm|            #define the name of the guest e.g. jenkins, jenkins1 etc
      guest.vm.provider "virtual box" do |vb|               #set provider for guest from yml file
        vb.cpus = guest['cpus']                             #set cpu for guest from yml file
        vb.memory = guest['memory']                         #set memory for guest from yml file
      guest_vm.vm.box = guest['box']                        #set OS for guest from yml file
      guest_vm.vm.network "private network", ip: guest['private_ip']                               #set ip for guest from yml file	
      unless guest['scripts'].nil?                                                                 #if no scripts, then run following code
        guest['scripts'].each do |script|                                                          #run scripts for guest from yml file
          guest_vm.vm.provision "shell", privileged: false, path: "vagrant_scripts/#{script}"      #load shell with specifed path

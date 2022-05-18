# dist linux utilisée
IMAGE_NAME ="bento/ubuntu-20.04"
NODE_NETWORK_BASE ="192.168.60"
VM_NAME = "ckanvm"

Vagrant.configure("2") do |config|
    # ckanvm server
    config.vm.boot_timeout = 600
    config.vm.define "ckanvm" do |ckanvm|
      ckanvm.vm.box =IMAGE_NAME
      ckanvm.vm.hostname = VM_NAME
      ckanvm.vm.box_url = IMAGE_NAME
      ckanvm.vm.network :private_network, ip: "#{NODE_NETWORK_BASE}.2"  
      # redirection de ports : port_vm --> port_machine_host
      ckanvm.vm.network "forwarded_port", guest: 80, host: 8090
      ckanvm.vm.network "forwarded_port", guest: 5000, host: 5000

      # Synchronisation des repertoires machine hôte et machine virtuelle 
      config.vm.synced_folder "C:/Users/", "/shared_rep"

      ckanvm.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
        #allocation RAM
        v.customize ["modifyvm", :id, "--memory", 2048]

        v.customize ["modifyvm", :id, "--name", VM_NAME]
        # allocation des CPUs
        v.customize ["modifyvm", :id, "--cpus", "2"]
      end
    end
   
    
end

#
# High availability Drupal distribution (test platform)
#-------------------------------------------------------------------------------
#
# This Vagrantfile is designed to test server components in the enclosed manifests
# relating to setting up a Drupal site.
#
Vagrant::Config.run do |config|

  #-----------------------------------------------------------------------------
  # General configurations

  vm_network_bridged   = false

  vm_box               = "precise64"
  vm_box_url           = "http://files.vagrantup.com/precise64.box"

  puppet_manifest_file = "site.pp"
  puppet_manifest_path = "puppet"
  puppet_module_path   = "#{puppet_manifest_path}/core/modules"
  puppet_options       = "--verbose" # NOTE: The --debug and --verbose options can be life savers!
  
  drupal_vm_cpus       = "1"
  drupal_vm_memory     = "512"
  
  percona_vm_cpus      = "1"
  percona_vm_memory    = "512"

  #-----------------------------------------------------------------------------
  # Drupal servers

  config.vm.define :drupal1 do |drupal1|  
    drupal1.vm.host_name = "vagrant-drupal1"
  
    drupal1.vm.box       = vm_box
    drupal1.vm.box_url   = vm_box_url

    if vm_network_bridged
      drupal1.vm.network :bridged
    else
      drupal1.vm.network :hostonly, "172.10.10.11"
    end
  
    drupal1.vm.customize ["modifyvm", :id, "--cpus", drupal_vm_cpus, "--memory", drupal_vm_memory]
  
    drupal1.vm.provision :puppet do |puppet|
      puppet.module_path    = puppet_module_path
      puppet.manifests_path = puppet_manifest_path
      puppet.manifest_file  = puppet_manifest_file
      puppet.options        = puppet_options
    end
  end
  
  #---  
  
  config.vm.define :drupal2 do |drupal2|  
    drupal2.vm.host_name = "vagrant-drupal2"
  
    drupal2.vm.box       = vm_box
    drupal2.vm.box_url   = vm_box_url

    if vm_network_bridged
      drupal2.vm.network :bridged
    else
      drupal2.vm.network :hostonly, "172.10.10.12"
    end
  
    drupal2.vm.customize ["modifyvm", :id, "--cpus", drupal_vm_cpus, "--memory", drupal_vm_memory]
  
    drupal2.vm.provision :puppet do |puppet|
      puppet.module_path    = puppet_module_path
      puppet.manifests_path = puppet_manifest_path
      puppet.manifest_file  = puppet_manifest_file
      puppet.options        = puppet_options   
    end
  end  

  #-----------------------------------------------------------------------------
  # Database servers

  config.vm.define :percona1 do |percona1|  
    percona1.vm.host_name = "vagrant-percona1"
  
    percona1.vm.box       = vm_box
    percona1.vm.box_url   = vm_box_url

    if vm_network_bridged
      percona1.vm.network :bridged
    else
      percona1.vm.network :hostonly, "172.10.20.11"
    end

    percona1.vm.customize ["modifyvm", :id, "--cpus", percona_vm_cpus, "--memory", percona_vm_memory]
  
    percona1.vm.provision :puppet do |puppet|
      puppet.module_path    = puppet_module_path
      puppet.manifests_path = puppet_manifest_path
      puppet.manifest_file  = puppet_manifest_file
      puppet.options        = puppet_options  
    end
  end
  
  #---
  
  config.vm.define :percona2 do |percona2|  
    percona2.vm.host_name = "vagrant-percona2"
  
    percona2.vm.box       = vm_box
    percona2.vm.box_url   = vm_box_url

    if vm_network_bridged
      percona2.vm.network :bridged
    else
      percona2.vm.network :hostonly, "172.10.20.12"
    end
 
    percona2.vm.customize ["modifyvm", :id, "--cpus", percona_vm_cpus, "--memory", percona_vm_memory]
  
    percona2.vm.provision :puppet do |puppet|
      puppet.module_path    = puppet_module_path
      puppet.manifests_path = puppet_manifest_path
      puppet.manifest_file  = puppet_manifest_file
      puppet.options        = puppet_options  
    end
  end
  
  #---
    
  config.vm.define :percona3 do |percona3|  
    percona3.vm.host_name = "vagrant-percona3"
  
    percona3.vm.box       = vm_box
    percona3.vm.box_url   = vm_box_url

    if vm_network_bridged
      percona3.vm.network :bridged
    else
      percona3.vm.network :hostonly, "172.10.20.13"
    end
 
    percona3.vm.customize ["modifyvm", :id, "--cpus", percona_vm_cpus, "--memory", percona_vm_memory]
  
    percona3.vm.provision :puppet do |puppet|
      puppet.module_path    = puppet_module_path
      puppet.manifests_path = puppet_manifest_path
      puppet.manifest_file  = puppet_manifest_file
      puppet.options        = puppet_options  
    end
  end  
end

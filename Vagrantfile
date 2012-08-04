#
# High availability Drupal distribution (test platform)
#-------------------------------------------------------------------------------
#
# This Vagrantfile is designed to test server components in the enclosed manifests
# relating to setting up a Drupal site.
#
Vagrant::Config.run do |config|

  #-----------------------------------------------------------------------------
  # Web servers

  config.vm.define :web1 do |web1_config|  
    web1_config.vm.host_name = "vagrant-web1"
  
    web1_config.vm.box       = "precise64"
    web1_config.vm.box_url   = "http://files.vagrantup.com/precise64.box"

    web1_config.vm.network :hostonly, "172.10.10.1"
    # web1_config.vm.network :bridged
  
    web1_config.vm.customize ["modifyvm", :id, "--cpus", "1", "--memory", "512"]
  
    web1_config.vm.provision :puppet do |puppet|
      puppet.module_path    = "puppet/modules"
      puppet.manifests_path = "puppet/manifests"
      puppet.manifest_file  = "site.pp"
      puppet.options        = "--verbose" # NOTE: The --debug and --verbose options can be life savers!   
    end
  end  
  
  config.vm.define :web2 do |web2_config|  
    web2_config.vm.host_name = "vagrant-web2"
  
    web2_config.vm.box       = "precise64"
    web2_config.vm.box_url   = "http://files.vagrantup.com/precise64.box"

    web2_config.vm.network :hostonly, "172.10.10.2"
    # web2_config.vm.network :bridged
  
    web2_config.vm.customize ["modifyvm", :id, "--cpus", "1", "--memory", "512"]
  
    web2_config.vm.provision :puppet do |puppet|
      puppet.module_path    = "puppet/modules"
      puppet.manifests_path = "puppet/manifests"
      puppet.manifest_file  = "site.pp"
      puppet.options        = "--verbose" # NOTE: The --debug and --verbose options can be life savers!   
    end
  end  

  #-----------------------------------------------------------------------------
  # Database servers

  config.vm.define :db1 do |db1_config|  
    db1_config.vm.host_name = "vagrant-db1"
  
    db1_config.vm.box       = "precise64"
    db1_config.vm.box_url   = "http://files.vagrantup.com/precise64.box"

    db1_config.vm.network :hostonly, "172.10.20.1"
    # db1_config.vm.network :bridged
  
    db1_config.vm.customize ["modifyvm", :id, "--cpus", "1", "--memory", "512"]
  
    db1_config.vm.provision :puppet do |puppet|
      puppet.module_path    = "puppet/modules"
      puppet.manifests_path = "puppet/manifests"
      puppet.manifest_file  = "site.pp"
      puppet.options        = "--verbose" # NOTE: The --debug and --verbose options can be life savers!   
    end
  end  
  
  config.vm.define :db2 do |db2_config|  
    db2_config.vm.host_name = "vagrant-db2"
  
    db2_config.vm.box       = "precise64"
    db2_config.vm.box_url   = "http://files.vagrantup.com/precise64.box"

    db2_config.vm.network :hostonly, "172.10.20.2"
    # db2_config.vm.network :bridged
  
    db2_config.vm.customize ["modifyvm", :id, "--cpus", "1", "--memory", "512"]
  
    db2_config.vm.provision :puppet do |puppet|
      puppet.module_path    = "puppet/modules"
      puppet.manifests_path = "puppet/manifests"
      puppet.manifest_file  = "site.pp"
      puppet.options        = "--verbose" # NOTE: The --debug and --verbose options can be life savers!   
    end
  end  
end

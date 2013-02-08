#
# Configurable Vagrant server environment (development platform)
#-------------------------------------------------------------------------------
#
# This Vagrantfile is designed to test server components
#
# => "puppet" directory should be a submodule with a bootstrap capable Puppet library.
# => "config" directory should be a submodule with a JSON configuration repository.
#

require 'coral_vagrant'

Vagrant::Config.run do |config|

  #-----------------------------------------------------------------------------
  # Server definitions (managed by ./config/cloud.json)

  cloud = Coral.init_vagrant(File.dirname(__FILE__))
  
  cloud.servers.each do |server_name, server|  
    config.vm.define server_name do |machine|    
      # Basic server settings      
      machine.vm.host_name = server.hostname
            
      machine.vm.box       = cloud.get('vm_box')
      machine.vm.box_url   = cloud.get('vm_box_url')
      
      # Network interfaces      
      if cloud.get('vm_network_bridged', false, :test)
        machine.vm.network :bridged
      else
        machine.vm.network :hostonly, server.public_ip
        
        unless server.virtual_ip.empty?
          machine.vm.network :hostonly, server.virtual_ip
        end
      end
     
      # Server NFS shares      
      cloud.servers[server_name].shares.each do |name, share|
        unless share.directory.empty? || share.remote_dir.empty?
          machine.vm.share_folder name, share.remote_dir, share.directory, :nfs => true
        end
      end
            
      # Server settings      
      vm_cpus   = cloud.search(server_name, 'vm_cpus', '1')
      vm_memory = cloud.search(server_name, 'vm_memory', '512')
      
      machine.vm.customize [ "modifyvm", :id, "--cpus", vm_cpus, "--memory", vm_memory ]
            
      # Puppet configuration
      puppet_manifest_path = cloud.get('puppet_manifest_path')
      puppet_module_path   = [] 
      cloud.get('puppet_module_path', [], :array).each do |module_path|
        puppet_module_path << File.join(puppet_manifest_path, module_path)
      end
      
      # Puppet provisioning      
      machine.vm.provision :puppet do |puppet|
        puppet.module_path    = puppet_module_path
        puppet.manifests_path = puppet_manifest_path
        puppet.manifest_file  = cloud.get('puppet_manifest_file')
        puppet.options        = cloud.search(server_name, 'puppet_options')
        puppet.facter         = cloud.search(server_name, 'facts')
      end
    end
  end
end

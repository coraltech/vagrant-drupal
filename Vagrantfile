
$config_path = Pathname.new("../config").realpath.to_s

Vagrant::Config.run do |config|
  config.vm.host_name = "panopoly"

  config.vm.box     = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :hostonly, "172.0.0.4"
  # config.vm.network :bridged
  
  config.vm.customize ["modifyvm", :id, "--cpus", "2", "--memory", "1024"]

  if File.exists?($config_path) then  
    config.vm.share_folder "config", "/var/git/config.git", $config_path, :nfs => (RUBY_PLATFORM =~ /linux/ or RUBY_PLATFORM =~ /darwin/)
  end

  config.vm.provision :puppet do |puppet|
    puppet.module_path    = "puppet/modules"
    puppet.manifests_path = "puppet/manifests"
    puppet.manifest_file  = "panopoly.pp"
    puppet.options        = "--verbose"    
  end
end

#
# Panopoly Drupal distribution
#-------------------------------------------------------------------------------
#
# This Vagrantfile is designed to test server components in the enclosed manifests
# relating to setting up a Drupal site.
#
# This path stores a copy of configurations that can locally emulate the
# internally managed cloud configurations without the cloud api's.

#
# All servers in the cluster should share the same $config_path.
#
$config_path = Pathname.new("/var/git/config.git").realpath.to_s


Vagrant::Config.run do |config|
  
  # Hostname controls which Puppet node is recognized.  This should match the 
  # name of the node in the puppet manifest file below.
  config.vm.host_name = "panopoly"

  config.vm.box     = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :hostonly, "172.0.0.4"
  # config.vm.network :bridged
  
  config.vm.customize ["modifyvm", :id, "--cpus", "2", "--memory", "1024"]

  # We NFS mount our coniguration directory so it appears internal to the server.
  # Work around for lack of server environment API (ie: Rackspace Cloud API).
  if File.exists?($config_path) then  
    config.vm.share_folder "config", "/var/git/config.git", $config_path, :nfs => (RUBY_PLATFORM =~ /linux/ or RUBY_PLATFORM =~ /darwin/)
  end

  config.vm.provision :puppet do |puppet|
    puppet.module_path    = "puppet/modules"
    puppet.manifests_path = "puppet/manifests"
    puppet.manifest_file  = "panopoly.pp"
    puppet.options        = "--verbose" # NOTE: The --debug and --verbose options can be lifesavers!   
  end
end

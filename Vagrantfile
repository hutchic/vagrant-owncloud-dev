# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.network "private_network", ip: "33.33.33.35"
  config.vm.synced_folder "webroot/", "/var/www",
  	owner: "www-data",
  	group: "www-data",
  	mount_options: ["dmode=770,fmode=770"]

  config.vm.provision :shell do |shell|
    shell.inline = "mkdir -p /etc/puppet/modules
      # once owncloud-dev::from_source is available from forge the lines below go away
      (puppet module list |grep  puppetlabs-vcsrepo) || puppet module install puppetlabs/vcsrepo
      (puppet module list |grep  puppetlabs-apache) || puppet module install puppetlabs/apache
      (puppet module list |grep  puppetlabs-mysql) || puppet module install puppetlabs/mysql
      (puppet module list |grep  example42-php) || puppet module install example42/php
      (puppet module list |grep  puppetlabs-git) || puppet module install puppetlabs/git
      (puppet module list |grep  mhuffnagle-make) || puppet module install mhuffnagle/make
      (puppet module list |grep  willdurand-composer) || puppet module install willdurand/composer
      apt-get update"
  end

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "manifests"
    puppet.manifest_file  = "default.pp"
    puppet.module_path = [ 'modules' ]
  end
end

# -*- mode: ruby -*-
# # vi: set ft=ruby :

$project_slug = "albin"
$ip_address = "192.168.70.10"

require 'fileutils'
Vagrant.require_version ">= 1.6.0"

Vagrant.configure("2") do |config|

  config.ssh.insert_key = false

  config.vm.box = "coreos-stable"
  config.vm.box_version = ">= 308.0.1"
  config.vm.box_url = "http://stable.release.core-os.net/amd64-usr/current/coreos_production_vagrant.json"

  config.vm.provider :virtualbox do |vb|
    vb.check_guest_additions = false
    vb.functional_vboxsf     = false
    vb.gui = false
    vb.memory = 1024
    vb.cpus = 1
    vb.name = "%s" % $project_slug
  end

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

  if Vagrant.has_plugin?("vagrant-hostsupdater")
    config.hostsupdater.remove_on_suspend = true
  end

  config.vm.hostname = "%s.dev" % $project_slug
  config.vm.network :private_network, ip: "%s" % $ip_address

  config.vm.synced_folder "./%s.dev" % $project_slug, "/home/core/%s" % $project_slug, create: true, :mount_options => ["dmode=777", "fmode=666"]

end

# -*- mode: ruby -*-
# vi: set ft=ruby :

# Copyright 2013 Zürcher Hochschule für Angewandte Wissenschaften
# All Rights Reserved.
#
#    Licensed under the Apache License, Version 2.0 (the "License"); you may
#    not use this file except in compliance with the License. You may obtain
#    a copy of the License at
#
#         http://www.apache.org/licenses/LICENSE-2.0
#
#    Unless required by applicable law or agreed to in writing, software
#    distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
#    WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
#    License for the specific language governing permissions and limitations
#    under the License.

dhostname = "grizzly.local"

 

Vagrant::Config.run do |config|

config.vm.boot_mode = :gui

  config.vm.define :devstack do |puppet_config|

    puppet_config.vm.box = "precise64"
    puppet_config.vm.box_url = "http://files.vagrantup.com/precise64.box"

    # puppet_config.vm.boot_mode = :gui
    #puppet_config.vm.network  :hostonly, "10.1.2.44" #:hostonly or :bridged - default is NAT
    puppet_config.vm.host_name = dhostname
    puppet_config.vm.customize ["modifyvm", :id, "--memory", 1024]
    puppet_config.ssh.max_tries = 100

    puppet_config.vm.provision :puppet do |grizzly_puppet|
      grizzly_puppet.pp_path = "/tmp/puppet-openstack"
      grizzly_puppet.module_path = "modules"
      grizzly_puppet.manifests_path = "manifests"
      grizzly_puppet.manifest_file = "site.pp"
      grizzly_puppet.facter = { "fqdn" => dhostname }
    end
  end
end

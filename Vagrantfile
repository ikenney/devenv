# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "devenv"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network :forwarded_port, guest: 3000, host: 3004
  config.vm.provision :chef_solo do |chef|
    chef.add_recipe 'apt'
    chef.add_recipe 'tmux'
    chef.add_recipe 'vim'
    chef.add_recipe 'git'
#    chef.add_recipe 'make'
#    chef.add_recipe 'ctags'
#    chef.add_recipe 'curl'
    chef.add_recipe 'dotmatrix'
    chef.add_recipe 'rvm::system'
    chef.add_recipe 'rvm::gem_package'

    chef.json = {
      :rvm => {
        :rubies => 'ruby-head',
        :group_users => 'vagrant',
        :default_ruby => 'ruby-head',
        :global_gems => [ 
          {name: 'bundler'},
          {name: 'rake'},
          {name: 'rails'}
        ]
      }
    }
  end
end
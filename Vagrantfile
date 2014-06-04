# -*- mode: ruby -*-
# vi: set ft=ruby :
#
# Copyright 2013 Ian Kenney
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
#
Vagrant.configure("2") do |config|
  config.vm.box = "ah_test"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.network :forwarded_port, guest: 3000, host: 3004
  config.vm.provision :chef_solo do |chef|
    chef.add_recipe 'apt'
    chef.add_recipe 'locale-uk'
    chef.add_recipe 'tmux'
    chef.add_recipe 'vim'
    chef.add_recipe 'git'
    chef.add_recipe 'dotmatrix'
    chef.add_recipe 'postgres-rails-db'
    chef.add_recipe 'rvm::system'
    chef.add_recipe 'rvm::vagrant'
    chef.add_recipe 'rvm::gem_package'
    chef.add_recipe 'heroku-toolbelt'
    chef.add_recipe 'nodejs'
    chef.json = {
      :locale => { :lang => "en_GB.utf8", :language => 'en_GB', :lc_all => 'en_GB.utf8' },
      :rvm => {
        :rubies => 'ruby-head',
        :group_users => 'vagrant',
        :default_ruby => 'ruby-head',
        :global_gems => [ 
          {name: 'bundler'},
          {name: 'rake'},
          {name: 'rails'}
        ]
      },
      :postgresql => {
        :password => { 
          "postgres" => "md59e7d9c011017f092d4412b3fb11c8126",
          "vagrant" => "md5873a21eb415f6dca5d4863cb0a4c330d"
        },
        :pg_hba   => [
          { :type => "local", :db => "all", :user => "postgres", :addr => "", :method => "trust"},
          { :type => "host", :db => "all", :user => "postgres", :addr => "127.0.0.1/32", :method => "trust"},
          { :type => "host", :db => "all", :user => "vagrant", :addr => "127.0.0.1/32", :method => "trust"}
        ]
      },
      :build_essential => {
        :compiletime => true
      }
    }
  end
end

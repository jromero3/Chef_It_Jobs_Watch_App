required_plugins = %w( vagrant-hostsupdater vagrant-berkshelf )
required_plugins.each do |plugin|
  exec "vagrant plugin install #{plugin};vagrant #{ARGV.join(" ")}" unless Vagrant.has_plugin? plugin || ARGV[0] == 'plugin'
end

Vagrant.configure("2") do |config|
  config.omnibus.chef_version = '14.12.9'
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "private_network", ip: "192.168.10.100"
  config.hostsupdater.aliases = ["development.local"]
  config.vm.synced_folder "app", "/home/ubuntu/app"
  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "It_Jobs_Watch_Cookook::default"
  end
end

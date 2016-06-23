nodes = [
  {
    :hostname => 'upalate-vagrant1',
    :boxname => 'upalate-vagrant1',
    :aliases => ['upalate-vagrant1.uapalte.me'],
    :ip => '172.16.70.25',
    :box => 'bento/ubuntu-14.04',
    :ram => '4096',
    :cpus => 2,
    :synced_folders => [
      { 
        :host => "/var/tmp/#{ENV['USER']}/build/",
        :guest => "/var/tmp/#{ENV['USER']}/build/",
        :create => true,
      },
    ],
  }
]

Vagrant.configure("2") do |config|

  config.ssh.insert_key = false

  if Vagrant.has_plugin?('vagrant-cachier')
    config.cache.enable :apt
  else
    printf("** Install vagrant-cachier plugin to speedup deploy: `vagrant plugin install vagrant-cachier`.**\n")
  end

  if Vagrant.has_plugin?('vagrant-hostmanager')
    config.hostmanager.enabled = true 
    config.hostmanager.manage_host = true
  else
    printf("** INstall vagrant-hostmanager plugin: `vagrant plugin install vagrant-hostmanager`.**\n`")
  end

  nodes.each do |node|
    config.vm.define node[:hostname] do |node_config|
      node_config.vm.box = node[:box]
      node_config.vm.hostname = node[:hostname]
      node_config.hostmanager.aliases = node[:aliases]
      node_config.vm.provider :virtualbox do |vb|
        vb.memory = node[:ram]
        vb.cpus = node[:cpus]
      end
    end
  end
end

$provision_shell_script = <<SCRIPT
apt-get -qy update
echo "Setting Timezone..."
echo "America/Los_Angeles" | sudo tee /etc/timezon
sudo dpkg-reconfigure --frontend noninteractive tzdata

SCRIPT

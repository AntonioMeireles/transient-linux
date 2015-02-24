# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

boxName = "rickard-von-essen/opscode_fedora-20"
vName = "fedoraLinux"
realUser = ENV['USER']

PERSISTENT_HOMEDIR = ENV['PERSISTENT_HOMEDIR'] || \
  File.join(File.dirname(__FILE__), "persistent")

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = boxName
  config.vm.define vName

  config.vm.network "private_network", ip: "10.73.25.11"

  if ARGV[0] == "ssh"
    config.ssh.username = realUser
  end

  config.ssh.insert_key = false

  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true

  config.vm.provider :parallels do |p|
    p.update_guest_tools = true
    # p.check_guest_tools = false
    p.memory = 4096
    p.cpus = 2
    p.optimize_power_consumption = false
  end

  config.vm.provision :ansible, :run => "always" do |ansible|
    ansible.playbook = "provisioning/bootstrap.ansible"
    ansible.extra_vars = { user: "#{realUser}" }
  end

  config.vm.synced_folder ".", "/vagrant", :disabled => true

  config.vm.synced_folder "#{PERSISTENT_HOMEDIR}", "/home/#{realUser}",
    # as this actually runs before the provisioner, the user won't be created on
    # 1st boot using the hardcoded uid to get around that
    owner: 1001,
    group: "vagrant"
end

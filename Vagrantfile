# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.network :forwarded_port, host: 5000, guest: 80

    # Enable provisioning with Ansible.
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "site.yml"
        # ansible.verbose = "v"

        ansible.groups = {
            "appservers" => ["default"]
        }

        ansible.extra_vars = {
            hostname: "vagrant.coolproject.webbylab.com",
            remote_user: "vagrant"
        }
    end
end

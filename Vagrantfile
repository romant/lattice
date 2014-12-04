VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision "shell" do |s|
    s.path = "install_from_tar"
    s.args = ENV["VAGRANT_DIEGO_EDGE_TAR_PATH"]
  end

  config.vm.provider "virtualbox" do |v, override|
    # dns resolution appears to be very slow in some environments; this fixes it
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    override.vm.network "private_network", ip: "192.168.11.11"

    # increase memory on provisioned vm to 4gb
    v.customize ["modifyvm", :id, "--memory", 4096]
  end

  config.vm.provider "vmware_fusion" do |v, override|
    override.vm.box = "casualjim/trusty-vagrant"
    override.vm.network "private_network", ip: "192.168.100.10"

    # increase memory on provisioned vm to 4gb
    v.vmx["memsize"] = "4096"
  end
end

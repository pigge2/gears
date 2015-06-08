Vagrant.configure("2") do |config|

  config.vm.box = "hashicorp/precise32"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "site.yml"
    ansible.groups = {
      "proxy" => ["frontend"],
      "backend" => ["node1", "node2", "node3"],
    }
  end


  config.vm.define "frontend" do |proxy|
    proxy.vm.hostname = "frontend"
    proxy.vm.network "private_network", ip: "192.168.35.10"

    # Will do this with roles in Ansible instead
    #config.vm.provision "ansible" do |ansible|
    #  ansible.playbook = "proxy.yml"
    #end

  end

#  Single node config
#  config.vm.define "node1" do |backend|
#    backend.vm.hostname = "node1"
#    backend.vm.network "private_network", ip: "192.168.35.11"
#  end


  (1..3).each do |i|
    config.vm.define "node#{i}" do |backend|
      backend.vm.hostname = "node#{i}"
      backend.vm.network "private_network", ip: "192.168.35.1#{i}"
    end
  end

end


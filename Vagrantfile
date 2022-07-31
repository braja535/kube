num_instances = 2
Vagrant.configure("2") do |config|
    #config.ssh.insert_key = false
    config.vm.box = "ubuntu/focal64"
    config.vm.provider "virtualbox" do |v|
        v.memory = 2048
     #   v.cpus = 2
    end
      
    config.vm.define "k8s-master" do |master|
        #master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.56.10"
        master.vm.hostname = "k8s-master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "kube-virtualbox/master-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.56.10",
            }
        end
    end

    (1..num_instances).each do |i|
        config.vm.define "node-#{i}" do |node|
            #node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.56.#{i + 10}"
            node.vm.hostname = "node-#{i}"
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "kube-virtualbox/node-playbook.yml"
                ansible.extra_vars = {
                    node_ip: "192.168.56.#{i + 10}",
                }
            end
        end
    end
end

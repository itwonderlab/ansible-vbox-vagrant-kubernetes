IMAGE_NAME = "bento/ubuntu-18.04"
K8S_NAME = "ditwl-k8s-01"
MASTERS_NUM = 1
MASTERS_MEM = 2048
MASTERS_CPU = 2

NODES_NUM = 2
IP_BASE = "192.168.50."

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = MASTERS_MEM
        v.cpus = MASTERS_CPU
    end

    (1..MASTERS_NUM).each do |i|      
        config.vm.define "k8s-m-#{i}" do |master|
            master.vm.box = IMAGE_NAME
            master.vm.network "private_network", ip: "192.168.50.#{i + 10}"
            #config.vm.network "forwarded_port", guest: 8080, host: 8080, protocol: "tcp"
            master.vm.hostname = "k8s-m-#{i}"
            master.vm.provision "ansible" do |ansible|
                ansible.playbook = "roles/k8s.yml"
                ansible.groups = {
                    "k8s-master" => ["k8s-m-[1:#{MASTERS_NUM}]"],
                    "k8s-node" => ["k8s-n-[1:#{NODES_NUM}]"]
                }
                #Redefine defaults
                ansible.extra_vars = {
                    k8s_cluster_name:       K8S_NAME,                    
                    k8s_master_admin_user:  "vagrant",
                    k8s_master_admin_group: "vagrant",
                    k8s_master_apiserver_advertise_address: "192.168.50.#{i + 10}",
                    k8s_master_node_name: "k8s-m-#{i}"
                }                
            end
        end
    end

    (1..NODES_NUM).each do |j|
        config.vm.define "k8s-n-#{j}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.50.#{j + 10 + MASTERS_NUM}"
            node.vm.hostname = "k8s-n-#{j}"
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "roles/k8s.yml"                
                ansible.groups = {
                    "k8s-master" => ["k8s-m-[1:#{MASTERS_NUM}]"],
                    "k8s-node" => ["k8s-n-[1:#{NODES_NUM}]"]
                }                    
                #Redefine defaults
                ansible.extra_vars = {
                    k8s_cluster_name:     K8S_NAME,
                    k8s_node_admin_user:  "vagrant",
                    k8s_node_admin_group: "vagrant"                    
                }
            end
        end
    end

end    
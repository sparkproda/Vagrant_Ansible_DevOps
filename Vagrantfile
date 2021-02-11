IMAGE_NAME = "bento/ubuntu-18.04"
N = 1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 8192
        v.cpus = 2
    end

    config.vm.box_check_update = false

    (1..N).each do |i|
        config.vm.define "devops-vm-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.disksize.size = '20GB'
            node.vm.network "private_network", ip: "192.168.77.#{i + 10}"
            node.vm.hostname = "devops-vm-#{i}"
            node.vm.provision "ansible" do |ansible|
                ansible.playbook="playbook.yaml"
                ansible.ask_vault_pass = true
            end
        end
    end
    
end    
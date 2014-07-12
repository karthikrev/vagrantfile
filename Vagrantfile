VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
   config.vm.provision "shell", inline: "echo Hello"
    machines = {
        "solo" => {"name" => "solo", "ip" => "33.33.33.10", "ram" => "4096", "cpu" => "1", "box" => "centos"},
        "client1" => {"name" => "client1", "ip" => "33.33.33.13", "ram" => "512", "cpu" => "1", "box" => "centos"},
        "client2" => {"name" => "client2", "ip" => "33.33.33.14", "ram" => "512", "cpu" => "1", "box" => "centos"},
        "server" => {"name" => "chef-server", "ip" => "33.33.33.2", "ram" => "4096", "cpu" => "2", "box" => "centos"},
    }
    machines.each_key do | machine |
        ip = machines[machine]['ip']
        mem = machines[machine]['ram']
        cpu = machines[machine]['cpu']
        hname = machines[machine]['name']
        box = machines[machine]['box']
        config.vm.define machine do | myvm |
            myvm.vm.provider :virtualbox do |vbox|
                vbox.customize [
                    'modifyvm', :id,
                    '--memory', mem,
                    '--cpus', cpu,
                    '--ioapic', 'on'
                ]
            end
            myvm.vm.box = box 
            myvm.vm.hostname = hname
            myvm.vm.network :private_network, :ip => ip
            #myvm.omnibus.chef_version = :latest
        end
    end
end

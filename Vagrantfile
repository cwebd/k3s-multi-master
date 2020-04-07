cluster = {
 "server1" => { 
   macaddress2: "7e522693e957",
   k3os_config: "config/server1/k3os/config.yaml"
},
 "server2" => {
   macaddress2: "224863aa8bde",
   k3os_config: "config/server2/k3os/config.yaml"
 },
 "server3" => { 
   macaddress2: "6eb0b992eb1b",
   k3os_config: "config/server3/k3os/config.yaml"
 }
}

Vagrant.configure("2") do |config|

  cluster.each_with_index do |(hostname, info), index|

    config.vm.define hostname do |cfg|
      cfg.vm.provider :virtualbox do |vb, override|
     
        cfg.vm.box = "cwebd/k3os"
        cfg.vm.box_version = "1.0.0"

        vb.customize ["modifyvm", :id,
          "--nic2", "bridged",
          "--bridgeadapter2", "em1",
          "--macaddress2", info[:macaddress2]
        ]
  
      end

      cfg.vm.provision "file", source: info[:k3os_config], destination: "/home/rancher/k3os-config.yaml"
      
      # K3os Configuration
      cfg.vm.provision "shell", inline: "if ! cmp -s /home/rancher/k3os-config.yaml /var/lib/rancher/k3os/config.yaml; then sudo cp /home/rancher/k3os-config.yaml /var/lib/rancher/k3os/config.yaml && reboot; fi", upload_path: "/home/rancher/provision-k3os-config.sh"
    end
  end


end

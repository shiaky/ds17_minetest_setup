# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  config.vm.box = "archlinux/archlinux"
  config.vm.network "forwarded_port", guest: 30000, host: 1337
  config.vm.network "public_network", mac: "080027ffffff", use_dhcp_assigned_default_route: true
  config.vm.hostname = "minetest"
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
  end

  config.vm.provision "shell", preserve_order: true, inline: "sudo pacman -Sy --noconfirm minetest-server"
   
  MINETEST_UID = 995
  MINETEST_GID = 995
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "mods", "/usr/share/minetest/mods", owner: MINETEST_UID, group: MINETEST_GID 
  config.vm.synced_folder "gamedata", "/var/lib/minetest/", owner: MINETEST_UID, group: MINETEST_GID
  config.vm.synced_folder "etcminetest", "/etc/minetest/", owner: MINETEST_UID, group: MINETEST_GID
  
  config.vm.provision "shell", run: "always", inline: <<-SHELL
      sudo systemctl stop minetest@datenspuren && echo 'Minetest server stopped'
    sudo systemctl start minetest@datenspuren && echo 'Minetest server started'
    sleep 5
    sudo find /var/lib/minetest -name "world.mt" -exec sudo sed -i '/^load_mod_/ s/ false/ true/' {} \\;
    sudo systemctl restart minetest@datenspuren && echo 'Minetest server restarted'
    sleep 5
    sudo systemctl status minetest@datenspuren
    ip addr show | grep -A2 -B2 08:00:27:ff:ff:ff
  SHELL

end

# sudo find /var/lib/minetest -name "world.mt" -exec sudo sed -i '/^load_mod_/ s/ false/ true/' {} \\;
# sudo sed -i '/^load_mod_/ s/ false/ true/' /var/lib/minetest/datenspuren/world.mt

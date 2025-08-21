Vagrant.configure("2") do |config|
  config.vbguest.installer_options = { allow_kernel_upgrade: false }
  config.vbguest.auto_update = false
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--cableconnected1", "on"]
    vb.customize ["modifyvm", :id, "--uart1", "0x3F8", "4"]
    vb.customize ["modifyvm", :id, "--uartmode1", "file", File::NULL]
    vb.memory = "2048"
  end

  hosts = [
    { name: "almalinux10", box: "almalinux/10-kitten-x86_64_v2" },
    { name: "noble", box: "bento/ubuntu-24.04" },
    { name: "trixie", box: "bento/debian-13" },
  ]

  hosts.each do |host|
    config.vm.define host[:name] do |node|
      node.vm.box = host[:box]
      node.ssh.insert_key = true
      node.ssh.key_type = "ed25519"
      node.vm.hostname = host[:name]
      node.vm.boot_timeout = 600
    end
  end
end

Vagrant.configure("2") do |config|
  # Define la box base para los servidores Debian
  config.vm.box = "debian/bookworm64"

  # Aprovisionamiento general para instalar bind9 en ambas VMs
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update -y
    sudo apt-get install -y bind9
  SHELL

  # Configuración para "venus"
  config.vm.define "venus" do |venus|
    venus.vm.hostname = "venus.sistema.test" 
    venus.vm.network "private_network", ip: "192.168.57.102"
  end 

  # Configuración para "tierra"
  config.vm.define "tierra" do |tierra|
    tierra.vm.hostname = "tierra.sistema.test" 
    tierra.vm.network "private_network", ip: "192.168.57.103"
  end
end

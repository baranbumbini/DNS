Vagrant.configure("2") do |config|
  
  config.vm.box = "debian/bookworm64" 

 
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update -y
    sudo apt-get install -y bind9


    echo 'zone "sistema.test" {' | sudo tee -a /etc/bind/named.conf.local
    echo '    type master;' | sudo tee -a /etc/bind/named.conf.local
    echo '    file "/etc/bind/db.sistema.test";' | sudo tee -a /etc/bind/named.conf.local
    echo '};' | sudo tee -a /etc/bind/named.conf.local

  
    echo 'zone "57.168.192.in-addr.arpa" {' | sudo tee -a /etc/bind/named.conf.local
    echo '    type master;' | sudo tee -a /etc/bind/named.conf.local
    echo '    file "/etc/bind/db.192";' | sudo tee -a /etc/bind/named.conf.local
    echo '};' | sudo tee -a /etc/bind/named.conf.local

   
    echo '\$TTL    604800' | sudo tee /etc/bind/db.sistema.test
    echo '@   IN  SOA ns1.sistema.test. admin.sistema.test. (' | sudo tee -a /etc/bind/db.sistema.test
    echo '             2     ; Serial' | sudo tee -a /etc/bind/db.sistema.test
    echo '            604800 ; Refresh' | sudo tee -a /etc/bind/db.sistema.test
    echo '             86400 ; Retry' | sudo tee -a /etc/bind/db.sistema.test
    echo '           2419200 ; Expire' | sudo tee -a /etc/bind/db.sistema.test
    echo '            7200 ) ; Negative Cache TTL' | sudo tee -a /etc/bind/db.sistema.test 
    echo '@   IN  NS  ns1.sistema.test.' | sudo tee -a /etc/bind/db.sistema.test
    echo 'ns1 IN  A   192.168.57.103' | sudo tee -a /etc/bind/db.sistema.test
    echo 'venus IN  A   192.168.57.102' | sudo tee -a /etc/bind/db.sistema.test


    echo '\$TTL    604800' | sudo tee /etc/bind/db.192
    echo '@   IN  SOA ns1.sistema.test. admin.sistema.test. (' | sudo tee -a /etc/bind/db.192
    echo '             2     ; Serial' | sudo tee -a /etc/bind/db.192
    echo '            604800 ; Refresh' | sudo tee -a /etc/bind/db.192
    echo '             86400 ; Retry' | sudo tee -a /etc/bind/db.192
    echo '           2419200 ; Expire' | sudo tee -a /etc/bind/db.192
    echo '            7200 ) ; Negative Cache TTL' | sudo tee -a /etc/bind/db.192  
    echo '@   IN  NS  ns1.sistema.test.' | sudo tee -a /etc/bind/db.192
    echo '103 IN  PTR venus.sistema.test.' | sudo tee -a /etc/bind/db.192

    echo 'zone "sistema.test" {' | sudo tee -a /etc/bind/named.conf.local
    echo '    type slave;' | sudo tee -a /etc/bind/named.conf.local
    echo '    file "/etc/bind/db.sistema.test";' | sudo tee -a /etc/bind/named.conf.local
    echo '    masters { 192.168.57.103; };' | sudo tee -a /etc/bind/named.conf.local
    echo '};' | sudo tee -a /etc/bind/named.conf.local

    echo 'zone "57.168.192.in-addr.arpa" {' | sudo tee -a /etc/bind/named.conf.local
    echo '    type slave;' | sudo tee -a /etc/bind/named.conf.local
    echo '    file "/etc/bind/db.192";' | sudo tee -a /etc/bind/named.conf.local
    echo '    masters { 192.168.57.103; };' | sudo tee -a /etc/bind/named.conf.local
    echo '};' | sudo tee -a /etc/bind/named.conf.local

    sudo systemctl restart bind9
  SHELL


  config.vm.define "venus" do |venus|
    venus.vm.hostname = "venus.sistema.test" 
    venus.vm.network "private_network", ip: "192.168.57.102"
  end 


  config.vm.define "tierra" do |tierra|
    tierra.vm.hostname = "tierra.sistema.test" 
    tierra.vm.network "private_network", ip: "192.168.57.103"
  end
end

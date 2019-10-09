# -*- mode: ruby -*-
# vi: set ft=ruby :

ubuntu_log_file = File.join(Dir.pwd, ".resources/tmp/ubuntu-bionic-18.04-cloudimg-console.log")

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/bionic64"
  
  config.vm.hostname = "bootcamp"

  config.vm.network "private_network", ip: "192.168.66.10"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--uartmode1", "file", ubuntu_log_file]
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.synced_folder "./code", "/var/www", 
    :mount_options => ["dmode=777", "fmode=777"], 
    :owner => 'vagrant', :group => 'www-data'

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    
    # [Bootstrap]

    apt-get update

    echo 'LANGUAGE="en_US.UTF-8"' >> /etc/default/locale
    echo 'LC_ALL="en_US.UTF-8"' >> /etc/default/locale

    apt-get install -y build-essential software-properties-common
    apt-get install -y curl wget tree unzip sqlite3
    
    # [Apache]

    apt-get install -y apache2

    a2enmod rewrite
    sed -i 's/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf

    service apache2 restart
    
    # [MySQL]

    apt-get install -y mysql-server 
    
    mysql -e "CREATE USER 'arkus'@'%' IDENTIFIED BY 'nexus';"
    mysql -e "GRANT ALL PRIVILEGES ON *.* TO 'arkus'@'%';"

    mysql -e "FLUSH PRIVILEGES;"

    # [PHP]
    
    apt-get install -y php7.2 php7.2-bcmath php7.2-cli php7.2-curl php7.2-gd php7.2-mbstring php7.2-mysql php7.2-sqlite3 php7.2-xml php7.2-zip
    sed -i "s/display_errors = .*/display_errors = On/" /etc/php/7.2/cli/php.ini
    sed -i "s/display_errors = .*/display_errors = On/" /etc/php/7.2/apache2/php.ini

    curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
    
    # [VirtualHost]

    wget -O virtualhost https://raw.githubusercontent.com/RoverWire/virtualhost/master/virtualhost.sh

    sed -i "s/.*Options Indexes FollowSymLinks MultiViews.*//" virtualhost
    sed -i '77s/<Directory \/>//' virtualhost
    sed -i '78s/AllowOverride All//' virtualhost
    sed -i '79s/<\/Directory>//' virtualhost

    chmod +x virtualhost && mv virtualhost /usr/local/bin
  SHELL

end

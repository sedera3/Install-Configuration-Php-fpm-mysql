# Install-Configuration-Php-fpm-mysql
# Pour la configuration de apache: https://doc.ubuntu-fr.org/apache2 
# LINUX (DEBIAN-UBUNTU)
- PHP 7.X-fpm
  - Installation php7.X-fpm
   Ubuntu:
    sudo add-apt-repository ppa:ondrej/php
    sudo apt update
   Debian:
    sudo apt install apt-transport-https lsb-release ca-certificates
    sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
    sudo sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
    sudo apt update
  
  - Configuration php7-X-fpm
    where is file configuration?
     php --ini | grep Loaded
    Edit file
     sudo nano file_path
     Make the follow in change
      cgi.fix_pathinfo=0
    Then, restart the php-fpm service:
      sudo systemctl restart php7.X-fpm.service
  
- MYSQL
  - Installation mysql
  
  - Configuration mysql
  
  


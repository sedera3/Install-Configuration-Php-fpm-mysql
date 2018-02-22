# Install-Configuration-Php-fpm-mysql
- Pour la configuration de apache: https://doc.ubuntu-fr.org/apache2 
# LINUX (DEBIAN-UBUNTU)
## PHP 7.X-fpm
  ### Installation php7.X-fpm
   - Ubuntu:
    - sudo add-apt-repository ppa:ondrej/php
    - sudo apt update
   - Debian:
    - sudo apt install apt-transport-https lsb-release ca-certificates
    - sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
    - sudo sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
    - sudo apt update
  
  ### Configuration php7-X-fpm
   - where is file configuration?
    - php --ini | grep Loaded
   - Edit file
    - sudo nano file_path
    - Make the follow in change: cgi.fix_pathinfo=0
    - Then, restart the php-fpm service: sudo systemctl restart php7.X-fpm.service
    
    Notice: active display_errors in php.ini 
    
 ## Apache
  ### Installation apache2
   - sudo apt-get install libapache2-mod-fastcgi
   
  ### Configuration apache2
    - Go to /etc/apache2/mods-available/fastcgi.conf
     - and modif: 
     ```
        <IfModule mod_fastcgi.c>
        
          AddHandler php7.2-fcgi .php
          Action php7.2-fcgi /php7.2-fcgi
          Alias /php7.2-fcgi /usr/lib/cgi-bin/php7.2-fcgi
          FastCgiExternalServer /usr/lib/cgi-bin/php7.2-fcgi -socket /var/run/php7.2-fpm.sock -pass-header  Authorization

          <Directory /usr/lib/cgi-bin>
              Require all granted
          </Directory>
        </IfModule>
    ```
  - Go to /etc/php/7.2/fpm/pool.d /www.conf
   - find listen in use: listen = (ex: /run/php/php7.2-fpm.sock)
   
  - Go to /etc/apache2/apache2.conf
   - and modif/add:
    ```
       <Directory /var/www/html/7.2>
       
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
        RewriteEngine On
        RewriteCond %{HTTP:Authorization} ^(.*)
        RewriteRule .* - [e=HTTP_AUTHORIZATION:%1]

        <FilesMatch ".+\.ph(p[3457]?|t|tml)$">
                SetHandler "proxy:unix:/run/php/php7.2-fpm.sock|fcgi://localhost"
        </FilesMatch>
    </Directory>
    ```
    Notice: you can used double server (ex: php5.6 / php7.2 ) 
   
   ```
      <Directory /var/www/html/5.6>
   
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted

        RewriteEngine On
        RewriteCond %{HTTP:Authorization} ^(.*)
        RewriteRule .* - [e=HTTP_AUTHORIZATION:%1]

        <FilesMatch ".+\.ph(p[3457]?|t|tml)$">
                SetHandler "proxy:unix:/run/php/php5.6-fpm.sock|fcgi://localhost"
        </FilesMatch>
</Directory>
   ```
   - Notice:
    - a2enmod = apache2 enable module

  
  ## MYSQL
  - Installation mysql
  
  - Configuration mysql
  
  


# apache_404_issue_fixed
404 Page not found issue fixed with .htaccess in apache2 server

## 1. Enabling an .htaccess File
sudo nano /etc/apache2/sites-available/your_domain.conf

## 2. Add the following Directory content block within the VirtualHost block:
 /etc/apache2/sites-available/your_domain.conf

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName your_domain
    ServerAlias www.your_domain
    DocumentRoot /var/www/your_domain
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined


<Directory /var/www/your_domain>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride All
                Order allow,deny
                allow from all
</Directory> 
</VirtualHost>

## 3. Restart Apache with the following command
sudo service apache2 restart

## 4. Creating the .htaccess File
sudo nano /var/www/your_domain/.htaccess

Add the following codes in .htaccess
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteCond %{REQUEST_FILENAME} !-l
  RewriteRule . /index.html [L]
</IfModule>

## 5. Restart Apache with the following command
sudo service apache2 restart

There you go! Now you all set, Try reloading your page you'll not find 404 error thereafter.

# ssl-crt

sudo apt-get install openssl -y 

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/librarymanagement.key -out /etc/ssl/certs/librarymanagement.crt

cp -r /var/www/Laravel-libraray-management-system/ /var/www/

cd /var/www/

sudo chown -R www-data.www-data /var/www/

sudo chmod -R 775 /var/www/

sudo nano /etc/apache2/sites-available/Laravel-libraray-management-system-ssl.conf

<VirtualHost 192.168.10.46:443>
DocumentRoot /var/www/
SSLEngine on
SSLCertificateFile /etc/ssl/certs/librarymanagement.crt
SSLCertificateKeyFile /etc/ssl/private/librarymanagement.key
servername www.librarymanagement.com
</VirtualHost>

a2ensite Laravel-libraray-management-system-ssl.conf

systemctl reload apache2

if
"AH00526: Syntax error on line 3 of /etc/apache2/sites-enabled/Laravel-libraray-management-system-ssl.conf:
Invalid command 'SSLEngine', perhaps misspelled or defined by a module not included in the server configuration
Action 'configtest' failed." this error occur then

sudo a2enmod ssl
sudo systemctl restart apache2

a2dissite default-ssl.conf

sudo systemctl restart apache2

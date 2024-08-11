# -Password-Protect-a-Subdomain-Using-.htaccess

# root@fawazpc:~# vi /etc/apache2/sites-available/fw.fawazpc.online.conf

<VirtualHost *:80>
    ServerName fw.fawazpc.online
    DocumentRoot /var/www/fw.fawazpc.online

    <Directory /var/www/fw.fawazpc.online>
        AllowOverride All
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/fw.fawazpc.online-error.log
    CustomLog ${APACHE_LOG_DIR}/fw.fawazpc.online-access.log combined
RewriteEngine on
RewriteCond %{SERVER_NAME} =fw.fawazpc.online
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>

## Create the Document Root Directory:
root@fawazpc:~#  mkdir -p /var/www/fw.fawazpc.online

## Enable the Virtual Host:
root@fawazpc:~# a2ensite fw.fawazpc.online.conf

Enabling site fw.fawazpc.online.
To activate the new configuration, you need to run:
  systemctl reload apache2
## Reload Apache to Apply the Changes:  
root@fawazpc:~#  systemctl reload apache2
## Reload Apache to Apply the Changes:
# root@fawazpc:~# vi /var/www/fw.fawazpc.online/.htaccess
AuthType Basic
AuthName "Restricted Access"
AuthUserFile /var/www/fw.fawazpc.online/.htpasswd
Require valid-user
~
~
:wq!

root@fawazpc:~# htpasswd -c /var/www/fw.fawazpc.online/.htpasswd fawaz

New password:
Re-type new password:
Adding password for user fawaz

## Obtain the SSL certificate:
root@fawazpc:~# certbot --apache -d fw.fawazpc.online
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Requesting a certificate for fw.fawazpc.online
Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/fw.fawazpc.online/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/fw.fawazpc.online/privkey.pem
This certificate expires on 2024-11-09.
These files will be updated when the certificate renews.
Certbot has set up a scheduled task to automatically renew this certificate in the background.

Deploying certificate
Successfully deployed certificate for fw.fawazpc.online to /etc/apache2/sites-available/fw.fawazpc.online-le-ssl.conf
Congratulations! You have successfully enabled HTTPS on https://fw.fawazpc.online

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
If you like Certbot, please consider supporting our work by:
 * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
 * Donating to EFF:                    https://eff.org/donate-le
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
root@fawazpc:~#

output:
        ![image](https://github.com/user-attachments/assets/147c4643-80b6-4f53-bab5-d2a17e2e3adc)



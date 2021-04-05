.. _ug_export:

Export data
-----------

By default, Poudriere stores the data in ``/usr/local/poudriere/data/`` ::

  [root@build /usr/home/admin]# tree -d -L 2 /usr/local/poudriere/data/
  /usr/local/poudriere/data/
  |-- cache
  |   |-- 12amd64-local-devel
  |   `-- 12arm7-local-devel
  |-- logs
  |   `-- bulk
  `-- packages
      |-- 12amd64-local-devel
      `-- 12arm7-local-devel

  8 directories


Configure a web-server, e.g. Apache ::

  [root@build /usr/local/etc]# cat /usr/local/etc/apache24/Includes/usr-local-poudriere-data.conf
  <Directory /usr/local/poudriere/data>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
  </Directory>

  [root@build /usr/local/etc]# cat /usr/local/etc/apache24/extra/build.example.com.conf
     <VirtualHost *:80>
     ServerName build.example.com
     DocumentRoot /usr/local/poudriere/data/
     </VirtualHost>

     <VirtualHost *:443>
     ServerName build.example.com
     DocumentRoot /usr/local/poudriere/data/
     SSLCertificateFile /usr/local/etc/ssl/certs/build.example.com.crt
     SSLCertificateKeyFile /usr/local/etc/ssl/private/build.example.com.key
     </VirtualHost>

.. _ug_build_export:

Export data
-----------

By default, Poudriere stores the data in ``/usr/local/poudriere/data/`` ::

   shell> tree -d -L 2 /usr/local/poudriere/data/
   /usr/local/poudriere/data/
   ├── cache
   │   └── 141Ramd64-default-devel
   ├── logs
   │   └── bulk
   └── packages
       └── 141Ramd64-default-devel

Configure a web-server. For example, Apache ::

   shell> cat /usr/local/etc/apache24/Includes/usr-local-poudriere-data.conf
   <Directory /usr/local/poudriere/data>
     Options Indexes FollowSymLinks
     AllowOverride All
     Require all granted
   </Directory>

   shell> cat /usr/local/etc/apache24/extra/build.example.com.conf
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

The web page ``https://build.example.com/`` should display the list ::

  Index of /

      .m/
      cache/
      logs/
      packages/

Navigate through the *packages*

``https://build.example.com/packages/141Ramd64-default-devel/`` ::

  Index of /packages/141Ramd64-default-devel

      Parent Directory
      .building/
      .buildname
      .jailversion
      .latest/
      .real_1618001637/
      All/
      Latest/
      meta.conf
      meta.txz
      packagesite.txz

and display the *packages*

``https://build.example.com/packages/141Ramd64-default-devel/All/`` ::

   Index of /packages/141Ramd64-default-devel/All

   Parent Directory
   autoconf-2.72.pkg
   autoconf-switch-20220527.pkg
   automake-1.17.pkg
   bash-5.2.32.pkg
   bison-3.8.2_2,1.pkg
   boehm-gc-8.2.6.pkg
   cmake-core-3.30.2.pkg
   curl-8.9.1.pkg
   db5-5.3.28_9.pkg
   docbook-1.5.pkg
   docbook-sgml-4.5_1.pkg
   docbook-xml-5.0_3.pkg
   docbook-xsl-1.79.1_1,1.pkg
   expat-2.6.2.pkg
   getopt-1.1.6_1.pkg
   git-2.46.0.pkg
   gmake-4.4.1.pkg
   gtar-1.35_1.pkg
   ...

Review the logs, if needed

``https://build.example.com/logs/bulk/141Ramd64-default-devel/`` ::

   Index of /logs/bulk/141Ramd64-default-devel

   Parent Directory
   .data.json
   2024-08-08_22h56m31s/
   latest-done/
   latest-per-pkg/
   latest/

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

The web page ``https://build.example.com/`` should display the list ::

  Index of /

      .m/
      cache/
      logs/
      packages/

Navigate through the *packages*, e.g. ``https://build.example.com/packages/12arm7-local-devel/`` ::

  Index of /packages/12arm7-local-devel

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

and display the *packages*, e.g. ``https://build.example.com/packages/12arm7-local-devel/All/`` ::

  Index of /packages/12arm7-local-devel/All

    Parent Directory
    apr-1.7.0.1.6.1_1.txz
    autoconf-2.69_3.txz
    autoconf-wrapper-20131203.txz
    automake-1.16.3.txz
    bash-5.1.4_1.txz
    bash-completion-2.11,2.txz
    bison-3.7.5,1.txz
    boehm-gc-8.0.4_1.txz
    ca_root_nss-3.63.txz
    curl-7.75.0.txz
    cvsps-2.1_2.txz
    db5-5.3.28_7.txz
    dhcpdump-1.8.txz
    docbook-1.5.txz
    docbook-sgml-4.5_1.txz
    docbook-xml-5.0_3.txz
    docbook-xsl-1.79.1_1,1.txz
    expat-2.2.10.txz
    gdbm-1.19.txz
    getopt-1.1.6.txz
    gettext-runtime-0.21.txz
    gettext-tools-0.21.txz
    git-2.31.1.txz
    glib-2.66.7_1,1.txz
    gmake-4.3_2.txz
    gmp-6.2.1.txz
    ...

Review the logs, if needed, e.g. ``https://build.example.com/logs/bulk/12arm7-local-devel/`` ::

  Index of /logs/bulk/12arm7-local-devel

      Parent Directory
      .data.json
      2021-04-03_21h04m45s/
      2021-04-08_22h07m13s/
      2021-04-08_23h01m24s/
      2021-04-09_20h55m10s/
      2021-04-09_21h57m50s/
      2021-04-09_22h53m58s/
      latest-done/
      latest-per-pkg/
      latest/

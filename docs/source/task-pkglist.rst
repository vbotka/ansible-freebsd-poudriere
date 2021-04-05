Create lists of ports
^^^^^^^^^^^^^^^^^^^^^

The lists of the ports will be used by Poudriere. See `man(8) poudriere-bulk <https://www.freebsd.org/cgi/man.cgi?query=poudriere-bulk&sektion=8&manpath=freebsd-release-ports>`_ ::

     -f file      Absolute path to a file which contains the list of ports to
                  build.  Ports must be specified in the form category/port
                  and shell-style comments are allowed.  Multiple -f file
                  arguments may be specified at once.

By default, the generation of the lists is enabled ::

  poudriere_pkglists: true

By default, no architecture is selected ::

  poudriere_pkg_arch: []

Set the required architectures that the packages will be built for, e.g. ::

  poudriere_pkg_arch: [amd64]

For the selected architectures set the lists of the dictionaries in
the variables `pkgdict_*.yml
<https://github.com/vbotka/ansible-freebsd-postinstall/tree/master/defaults/main>`_
and, optionally, disable some of the lists, e.g. ::

  pkglist_enable_amd64:
    apcups: false
    linux: false
    devel: false
    joomla: false
    yazvs: false
    nginx: false
    docker: false
    snmpd: false

Create the lists ::

  shell> ansible-playbook pb.yml -t poudriere_pkglists -e poudriere_pkglists=true

Review the created lists of ports ::

  [root@build /usr/home/admin]# tree /usr/local/etc/poudriere.d/
  /usr/local/etc/poudriere.d/
  |-- jails
  |   `-- 12amd64
  |       |-- arch
  |       |-- method
  |       |-- mnt
  |       |-- timestamp
  |       `-- version
  |-- pkglist_amd64
  |   |-- ansible
  |   |-- apache
  |   |-- dhcp
  |   |-- dns
  |   |-- hostap
  |   |-- integrity
  |   |-- jail
  |   |-- leutils
  |   |-- mailserver
  |   |-- mailserver_sieve
  |   |-- mailserver_spamassasin
  |   |-- mcrypt
  |   |-- minimal
  |   |-- mysql
  |   |-- mysql_extra
  |   |-- pf
  |   |-- php
  |   |-- postinstall
  |   |-- poudriere
  |   |-- procmail
  |   |-- python
  |   |-- roundcube
  |   |-- roundcube_aspell
  |   |-- rsnapshot
  |   |-- security
  |   |-- smart
  |   |-- ssmtp
  |   `-- wpa_supplicant
  |-- pkglist_amd64.disabled
  |   |-- apcups
  |   |-- devel
  |   |-- docker
  |   |-- joomla
  |   |-- linux
  |   |-- nginx
  |   |-- snmpd
  |   `-- yazvs
  `-- ports
      `-- local
          |-- created_fs
          |-- method
          |-- mnt
          `-- timestamp


.. seealso::
   * Default packages' dictionaries in `pkgdict_*.yml <https://github.com/vbotka/ansible-freebsd-postinstall/tree/master/defaults/main>`_

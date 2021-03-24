Configure Poudriere
===================

By default, the configuration of Poudriere is enabled ::

  poudriere_conf: true

Read FreeBSD Porter's Handbook `10.5.2. Setting Up Poudriere
<https://docs.freebsd.org/en/books/porters-handbook/#testing-poudriere>`_ and see the sample
``/usr/local/etc/poudriere.conf.sample``. Customize the variables ``poudriere_conf_*`` and display
the the current values ::

  shell> ansible-playbook pb.yml -t poudriere_debug -e poudriere_debug=true

  ...
  TASK [vbotka.freebsd_poudriere : Poudriere Debug] ************************************************
  ok: [build.example.com] =>
    msg:
  ...
    - poudriere_conf_file [/usr/local/etc/poudriere.conf]
    - poudriere_conf_dir [/usr/local/etc/poudriere.d]
    - poudriere_conf_NO_ZFS [no]
    - poudriere_conf_ZPOOL [zroot]
    - poudriere_conf_ZROOTFS [/poudriere]
    - poudriere_conf_FREEBSD_HOST [https://download.freebsd.org]
    - poudriere_conf_RESOLV_CONF [/etc/resolv.conf]
    - poudriere_conf_BASEFS [/usr/local/poudriere]
    - poudriere_conf_POUDRIERE_DATA [/usr/local/poudriere/data]
    - poudriere_conf_USE_PORTLINT [no]
    - poudriere_conf_USE_TMPFS [no]
    - poudriere_conf_DISTFILES_CACHE [/usr/ports/distfiles]
    - poudriere_conf_PKG_REPO_SIGNING_KEY [/usr/local/etc/ssl/private/build.example.com.key]
    - poudriere_conf_URL_BASE [build.example.com]
    - poudriere_conf_CHECK_CHANGED_OPTIONS [verbose]
    - poudriere_conf_CHECK_CHANGED_DEPS [yes]
  ...

Configure Poudriere ::

  shell> ansible-playbook pb.yml -t poudriere_conf -e poudriere_conf=true

Review the created configuration ::

  [root@build /usr/home/admin]# cat /usr/local/etc/poudriere.conf
  # Ansible managed

  ZPOOL=zroot
  NO_ZFS=no
  ZROOTFS=/poudriere
  FREEBSD_HOST=https://download.freebsd.org
  RESOLV_CONF=/etc/resolv.conf
  BASEFS=/usr/local/poudriere
  POUDRIERE_DATA=/usr/local/poudriere/data
  USE_PORTLINT=no
  USE_TMPFS=no
  DISTFILES_CACHE=/usr/ports/distfiles
  PKG_REPO_SIGNING_KEY=/usr/local/etc/ssl/private/build.example.com.key
  URL_BASE=http://build.example.com/
  CHECK_CHANGED_OPTIONS=verbose
  CHECK_CHANGED_DEPS=yes

  # EOF


.. seealso::
   * Source code :ref:`as_conf.yml`
   * Template :ref:`as_template_poudriere.conf.j2`
   * FreeBSD Porter's Handbook  `10.5.2. Setting Up Poudriere <https://docs.freebsd.org/en/books/porters-handbook/#testing-poudriere>`_

Configure Poudriere
^^^^^^^^^^^^^^^^^^^

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
    - poudriere_conf [True]
    - poudriere_conf_file [/usr/local/etc/poudriere.conf]
    - poudriere_conf_template [poudriere.conf2.j2]
    - poudriere_conf_dir [/usr/local/etc/poudriere.d]
    - poudriere_conf_dirs
    - '-   dir: /usr/ports/distfiles'
    - '    group: wheel'
    - '    mode: ''0755'''
    - '    owner: root'
    - ''
    - poudriere_conf_zpool [zroot]
    - poudriere_conf_no_zfs [no]
    - poudriere_conf_zrootfs [/poudriere]
    - poudriere_conf_freebsd_host [https://download.freebsd.org]
    - poudriere_conf_resolv_conf [/etc/resolv.conf]
    - poudriere_conf_basefs [/usr/local/poudriere]
    - poudriere_conf_svn_host [svn.FreeBSD.org]
    - poudriere_conf_poudriere_data [/usr/local/poudriere/data]
    - poudriere_conf_use_portlint [no]
    - poudriere_conf_use_tmpfs [no]
    - poudriere_conf_distfiles_cache [/usr/ports/distfiles]
    - poudriere_conf_url_base [http://build.example.com/]
    - poudriere_conf_check_changed_options [verbose]
    - poudriere_conf_check_changed_deps [yes]
    - poudriere_conf_data
    - 'BASEFS: /usr/local/poudriere'
    - 'BUILDER_HOSTNAME: build'
    - 'CHECK_CHANGED_DEPS: ''yes'''
    - 'CHECK_CHANGED_OPTIONS: verbose'
    - 'DISTFILES_CACHE: /usr/ports/distfiles'
    - 'FREEBSD_HOST: https://download.freebsd.org'
    - 'NOLINUX: ''yes'''
    - 'NO_ZFS: ''no'''
    - 'PKG_REPO_SIGNING_KEY: /usr/local/etc/ssl/private/build.example.com-sk.key'
    - 'POUDRIERE_DATA: /usr/local/poudriere/data'
    - 'PRESERVE_TIMESTAMP: ''yes'''
    - 'RESOLV_CONF: /etc/resolv.conf'
    - 'SVN_HOST: svn.FreeBSD.org'
    - 'URL_BASE: http://build.example.com/'
    - 'USE_COLORS: ''yes'''
    - 'USE_PORTLINT: ''no'''
    - 'USE_TMPFS: ''no'''
    - 'ZPOOL: zroot'
    - 'ZROOTFS: /poudriere'
  ...

Configure Poudriere ::

  shell> ansible-playbook pb.yml -t poudriere_conf -e poudriere_conf=true

Review the configuration

.. literalinclude:: example-conf.txt
   :language: sh
   :linenos:
   :emphasize-lines: 1

.. seealso::
   * Source code :ref:`as_conf.yml`
   * Template :ref:`as_template_poudriere.conf.j2`
   * FreeBSD Porter's Handbook  `10.5.2. Setting Up Poudriere <https://docs.freebsd.org/en/books/porters-handbook/#testing-poudriere>`_

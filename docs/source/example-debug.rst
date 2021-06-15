.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_debug -e poudriere_debug=true

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Poudriere Debug] ************************************************************************************
   ok: [build.example.com] => 
     msg:
     - ansible_architecture [amd64]
     - ansible_os_family [FreeBSD]
     - ansible_distribution [FreeBSD]
     - ansible_distribution_major_version [12]
     - ansible_distribution_version [12.2]
     - ansible_distribution_release [12.2-RELEASE]
     - ansible_python_version [3.7.9]
     - ''
     - freebsd_install_method [packages]
     - freebsd_use_packages [True]
     - freebsd_install_retries [3]
     - freebsd_install_delay [5]
     - ''
     - poudriere_install [False]
     - poudriere_dirs [True]
     - poudriere_key [True]
     - poudriere_cert [False]
     - poudriere_conf [True]
     - poudriere_pkglists [True]
     - poudriere_options [False]
     - poudriere_make [True]
     - poudriere_backup_conf [True]
     - ''
     - poudriere_packages
     - '- ports-mgmt/poudriere'
     - '- ports-mgmt/portmaster'
     - '- devel/ccache'
     - ''
     - poudriere_packages_cert
     - '- security/py-openssl'
     - '- security/py-acme-tiny'
     - ''
     - poudriere_owner [root]
     - poudriere_group [wheel]
     - poudriere_mode [0644]
     - poudriere_mode_dir [0755]
     - poudriere_dirs [True]
     - poudriere_ssl_dir [/usr/local/etc/ssl]
     - poudriere_ssl_dir_mode [0755]
     - poudriere_ssl_private_dir [/usr/local/etc/ssl/private]
     - poudriere_ssl_private_dir_mode [0700]
     - poudriere_ssl_private_key_mode [0600]
     - poudriere_ssl_dirs
     - '- /usr/local/etc/ssl'
     - '- /usr/local/etc/ssl/crt'
     - '- /usr/local/etc/ssl/csr'
     - ''
     - poudriere_key [True]
     - poudriere_key_size [4096]
     - poudriere_key_type [RSA]
     - poudriere_key_cmd [openssl rsa -in /usr/local/etc/ssl/private/build.example.com-sk.key -pubout -out /usr/local/etc/ssl/crt/build.example.com-sk.crt]
     - poudriere_key_crt [/usr/local/etc/ssl/crt/build.example.com-sk.crt]
     - poudriere_conf_PKG_REPO_SIGNING_KEY [/usr/local/etc/ssl/private/build.example.com-sk.key]
     - ''
     - poudriere_cert [False]
     - poudriere_cert_cn [build.example.com]
     - poudriere_cert_key [/usr/local/etc/ssl/private/build.example.com.key]
     - poudriere_cert_csr [/usr/local/etc/ssl/csr/build.example.com.csr]
     - poudriere_cert_path [/usr/local/etc/ssl/certs/build.example.com.crt]
     - ''
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
     - ''
     - poudriere_pkglists [True]
     - poudriere_pkglist_dir [/usr/local/etc/poudriere.d/pkglist]
     - poudriere_pkg_arch [amd64]
     - ''
     - poudriere_options [False]
     - poudriere_make [True]
     - poudriere_make_file [/usr/local/etc/poudriere.d/make.conf]
     - poudriere_make_conf
     - '- "OPTIONS_UNSET+=\t\t\tDOCS NLS X11 EXAMPLES"'
     - '- "OPTIONS_UNSET+=\t\t\tGSSAPI_BASE KRB_BASE KERBEROS"'
     - '- "OPTIONS_SET+=\t\t\tGSSAPI_NONE KRB_NONE"'
     - '- "DEFAULT_VERSIONS+=\t\temacs=nox"'
     - '- "DEFAULT_VERSIONS+=\t\tphp=7.4"'
     - '- "DEFAULT_VERSIONS+=\t\tssl=openssl"'
     - ''

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

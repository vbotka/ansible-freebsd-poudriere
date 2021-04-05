.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_debug -e poudriere_debug=true

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Poudriere Debug] ******************************************************
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
     - poudriere_cert [False]
     - poudriere_conf [True]
     - poudriere_pkglists [True]
     - poudriere_make [False]
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
     - poudriere_ssl_dir [/usr/local/etc/ssl]
     - poudriere_ssl_dir_mode [0755]
     - poudriere_ssl_private_dir_mode [0700]
     - poudriere_ssl_private_key_mode [0600]
     - poudriere_cert_CN [build.example.com]
     - poudriere_csr_path [/usr/local/etc/ssl/csr/build.example.com.csr]
     - poudriere_cert_path [/usr/local/etc/ssl/certs/build.example.com.crt]
     - poudriere_cert_dirs
     - '-   dir: /usr/local/etc/ssl'
     - '    group: wheel'
     - '    mode: ''0755'''
     - '    owner: root'
     - '-   dir: /usr/local/etc/ssl/crt'
     - '    group: wheel'
     - '    mode: ''0755'''
     - '    owner: root'
     - '-   dir: /usr/local/etc/ssl/csr'
     - '    group: wheel'
     - '    mode: ''0755'''
     - '    owner: root'
     - '-   dir: /usr/local/etc/ssl/private'
     - '    group: wheel'
     - '    mode: ''0700'''
     - '    owner: root'
     - ''
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
     - poudriere_conf_dirs
     - '-   dir: /usr/ports/distfiles'
     - '    group: wheel'
     - '    mode: ''0755'''
     - '    owner: root'
     - ''
     - poudriere_make_file [/usr/local/etc/poudriere.d/make.conf]
     - poudriere_make_conf
     - '[]'
     - ''
     - poudriere_pkglist_dir [/usr/local/etc/poudriere.d/pkglist]
     - poudriere_pkg_arch [amd64]
     - ''

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

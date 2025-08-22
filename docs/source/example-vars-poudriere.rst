.. code-block:: yaml
   :caption: host_vars/build.example.com/poudriere.yml
   :linenos:
   :force:

   ---
   poudriere_install: false

   # cert
   poudriere_cert_cn: build.example.com
   poudriere_cert_key: "{{ poudriere_ssl_dir }}/private/{{ poudriere_cert_cn }}.key"
   poudriere_cert_csr: "{{ poudriere_ssl_dir }}/csr/{{ poudriere_cert_cn }}.csr"
   poudriere_cert_path: "{{ poudriere_ssl_dir }}/certs/{{ poudriere_cert_cn }}.crt"

   # key
   poudriere_key_crt: "{{ poudriere_ssl_dir }}/crt/{{ poudriere_cert_cn }}-sk.crt"
   poudriere_conf_pkg_repo_signing_key: "{{ poudriere_ssl_dir }}/private/{{ poudriere_cert_cn }}-sk.key"

   # conf
   poudriere_conf_template: poudriere.conf2.j2
   poudriere_conf_url_base: http://build.example.com
   poudriere_conf_no_zfs: "no"
   poudriere_conf_zpool: zroot
   poudriere_conf_use_tmpfs: "no"
   poudriere_conf_data:
     ZPOOL: "{{ poudriere_conf_zpool }}"
     NO_ZFS: "{{ poudriere_conf_no_zfs }}"
     ZROOTFS: "{{ poudriere_conf_zrootfs }}"
     FREEBSD_HOST: "{{ poudriere_conf_freebsd_host }}"
     RESOLV_CONF: "{{ poudriere_conf_resolv_conf }}"
     BASEFS: "{{ poudriere_conf_basefs }}"
     SVN_HOST: "{{ poudriere_conf_svn_host }}"
     POUDRIERE_DATA: "{{ poudriere_conf_poudriere_data }}"
     USE_PORTLINT: "{{ poudriere_conf_use_portlint }}"
     USE_TMPFS: "{{ poudriere_conf_use_tmpfs }}"
     DISTFILES_CACHE: "{{ poudriere_conf_distfiles_cache }}"
     PKG_REPO_SIGNING_KEY: "{{ poudriere_conf_pkg_repo_signing_key }}"
     URL_BASE: "{{ poudriere_conf_url_base }}"
     CHECK_CHANGED_OPTIONS: "{{ poudriere_conf_check_changed_options }}"
     CHECK_CHANGED_DEPS: "{{ poudriere_conf_check_changed_deps }}"
     NOLINUX: "yes"
     USE_COLORS: "yes"
     PRESERVE_TIMESTAMP: "yes"
     BUILDER_HOSTNAME: "build"

   # architecture
   poudriere_pkg_arch: [amd64]

   # make
   poudriere_make_conf:
     - "OPTIONS_UNSET+=\t\t\tDOCS NLS X11 EXAMPLES"
     - "OPTIONS_UNSET+=\t\t\tGSSAPI_BASE KRB_BASE KERBEROS"
     - "OPTIONS_SET+=\t\t\tGSSAPI_NONE KRB_NONE"
     - "DEFAULT_VERSIONS+=\t\temacs=nox"
     - "DEFAULT_VERSIONS+=\t\tphp=8.3"
     - "DEFAULT_VERSIONS+=\t\tssl=openssl"

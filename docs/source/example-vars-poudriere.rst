.. code-block:: bash
   :emphasize-lines: 1
   :linenos:

   shell> cat host_vars/build.example.com/poudriere.yml
   ---
   poudriere_install: false

   # cert
   poudriere_cert_CN: build.example.com
   poudriere_cert_key: "{{ poudriere_ssl_dir }}/private/{{ poudriere_cert_CN }}.key"
   poudriere_cert_csr: "{{ poudriere_ssl_dir }}/csr/{{ poudriere_cert_CN }}.csr"
   poudriere_cert_path: "{{ poudriere_ssl_dir }}/certs/{{ poudriere_cert_CN }}.crt"

   # key
   poudriere_key_crt: "{{ poudriere_ssl_dir }}/crt/{{ poudriere_cert_CN }}-sk.crt"
   poudriere_conf_PKG_REPO_SIGNING_KEY: "{{ poudriere_ssl_dir }}/private/{{ poudriere_cert_CN }}-sk.key"

   # conf
   poudriere_conf_template: poudriere.conf2.j2
   poudriere_conf_URL_BASE: http://build.example.com
   poudriere_conf_NO_ZFS: "no"
   poudriere_conf_ZPOOL: zroot
   poudriere_conf_USE_TMPFS: "no"
   poudriere_conf_data:
     ZPOOL: "{{ poudriere_conf_ZPOOL }}"
     NO_ZFS: "{{ poudriere_conf_NO_ZFS }}"
     ZROOTFS: "{{ poudriere_conf_ZROOTFS }}"
     FREEBSD_HOST: "{{ poudriere_conf_FREEBSD_HOST }}"
     RESOLV_CONF: "{{ poudriere_conf_RESOLV_CONF }}"
     BASEFS: "{{ poudriere_conf_BASEFS }}"
     SVN_HOST: "{{ poudriere_conf_SVN_HOST }}"
     POUDRIERE_DATA: "{{ poudriere_conf_POUDRIERE_DATA }}"
     USE_PORTLINT: "{{ poudriere_conf_USE_PORTLINT }}"
     USE_TMPFS: "{{ poudriere_conf_USE_TMPFS }}"
     DISTFILES_CACHE: "{{ poudriere_conf_DISTFILES_CACHE }}"
     PKG_REPO_SIGNING_KEY: "{{ poudriere_conf_PKG_REPO_SIGNING_KEY }}"
     URL_BASE: "{{ poudriere_conf_URL_BASE }}"
     CHECK_CHANGED_OPTIONS: "{{ poudriere_conf_CHECK_CHANGED_OPTIONS }}"
     CHECK_CHANGED_DEPS: "{{ poudriere_conf_CHECK_CHANGED_DEPS }}"
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
     - "DEFAULT_VERSIONS+=\t\tphp=7.4"
     - "DEFAULT_VERSIONS+=\t\tssl=openssl"

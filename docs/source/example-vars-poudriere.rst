.. code-block:: bash
   :emphasize-lines: 1,3-5
   :linenos:

   shell> cat host_vars/build.example.com/poudriere.yml
   ---
   poudriere_install: false
   poudriere_cert: false
   poudriere_make: false
   poudriere_cert_CN: build.example.com
   poudriere_conf_URL_BASE: build.example.com
   poudriere_conf_PKG_REPO_SIGNING_KEY: "{{ poudriere_ssl_dir }}/private/{{ poudriere_cert_CN }}.key"
   poudriere_conf_NO_ZFS: "no"
   poudriere_conf_ZPOOL: zroot
   poudriere_conf_USE_TMPFS: "no"
   poudriere_pkg_arch: [amd64]
   poudriere_csr_path: "{{ poudriere_ssl_dir }}/csr/{{ poudriere_cert_CN }}.csr"
   poudriere_cert_path: "{{ poudriere_ssl_dir }}/crt/{{ poudriere_cert_CN }}.crt"

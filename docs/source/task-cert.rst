Generate SSL certificate
^^^^^^^^^^^^^^^^^^^^^^^^

The generation of the certificate is not idempotent. Therefor, it is disabled by default ::

  poudriere_cert: false

The best practice is to create the certificate after the installation of the packages and keep it
disabled in the configuration ::

  shell> ansible-playbook pb.yml -t poudriere_cert -e poudriere_cert=true

By default, the names of the certificate's files are ``poudriere.*`` ::

  poudriere_ssl_dir: /usr/local/etc/ssl
  poudriere_conf_PKG_REPO_SIGNING_KEY: "{{ poudriere_ssl_dir }}/private/poudriere.pem"
  poudriere_csr_path: "{{ poudriere_ssl_dir }}/csr/poudriere.csr"
  poudriere_cert_path: "{{ poudriere_ssl_dir }}/crt/poudriere.crt"

Optionally, change the paths and names of the files, e.g. ::

  poudriere_cert_CN: build.example.com
  poudriere_conf_PKG_REPO_SIGNING_KEY: "{{ poudriere_ssl_dir }}/private/{{ poudriere_cert_CN }}.key"
  poudriere_csr_path: "{{ poudriere_ssl_dir }}/csr/{{ poudriere_cert_CN }}.csr"
  poudriere_cert_path: "{{ poudriere_ssl_dir }}/certs/{{ poudriere_cert_CN }}.crt"

Review the created files, ownership, and the permissions ::

  [root@build /usr/home/admin]# tree /usr/local/etc/ssl/
  /usr/local/etc/ssl/
  |-- cert.pem
  |-- cert.pem.sample -> ../../share/certs/ca-root-nss.crt
  |-- certs
  |   `-- build.example.com.crt
  |-- crt
  |-- csr
  |   `-- build.example.com.csr
  `-- private
      `-- build.example.com.key

.. seealso::

   * Source code :ref:`as_cert.yml`

Generate SSL certificate
^^^^^^^^^^^^^^^^^^^^^^^^

The generation of the SSL certificate for the web server is disabled by default ::

   poudriere_cert: false

By default, the names of the files are ``poudriere.key`` and  ``poudriere.crt`` ::

   poudriere_ssl_dir: /usr/local/etc/ssl
   poudriere_ssl_private_dir: /usr/local/etc/ssl/private
   poudriere_cert_key: "{{ poudriere_ssl_private_dir }}/poudriere.key"
   poudriere_csr_path: "{{ poudriere_ssl_dir }}/csr/poudriere.csr"
   poudriere_cert_path: "{{ poudriere_ssl_dir }}/crt/poudriere.crt"

Optionally, change the paths and names of the files. For example, ::

   poudriere_cert_cn: build.example.com
   poudriere_cert_key: "{{ poudriere_ssl_private_dir }}/{{ poudriere_cert_cn }}.key"
   poudriere_cert_csr: "{{ poudriere_ssl_dir }}/csr/{{ poudriere_cert_cn }}.csr"
   poudriere_cert_path: "{{ poudriere_ssl_dir }}/certs/{{ poudriere_cert_cn }}.crt"

Optionally, enable and generate the SSL certificate ::

   shell> ansible-playbook pb.yml -t poudriere_cert -e poudriere_cert=true

Take a look at the created files, ownership, and the permissions

.. literalinclude:: example-cert-tree.txt
   :language: sh
   :linenos:
   :emphasize-lines: 1

.. seealso::

   * Source code :ref:`as_cert.yml`

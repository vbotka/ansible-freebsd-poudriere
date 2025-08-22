.. _task_cert:

Generate SSL certificate
^^^^^^^^^^^^^^^^^^^^^^^^

.. index:: single: SSL; Tasks/Generate SSL certificate
.. index:: single: poudriere_cert; Tasks/Generate SSL certificate
.. index:: single: certificate; Tasks/Generate SSL certificate

By default, do not  generate the SSL certificate for the web server

.. code-block:: yaml

   poudriere_cert: false

By default, the names of the files are ``poudriere.key`` and  ``poudriere.crt``

.. code-block:: yaml

   poudriere_ssl_dir: /usr/local/etc/ssl
   poudriere_ssl_private_dir: /usr/local/etc/ssl/private
   poudriere_cert_key: "{{ poudriere_ssl_private_dir }}/poudriere.key"
   poudriere_csr_path: "{{ poudriere_ssl_dir }}/csr/poudriere.csr"
   poudriere_cert_path: "{{ poudriere_ssl_dir }}/crt/poudriere.crt"

Optionally, change the paths and names of the files. For example,

.. code-block:: yaml

   poudriere_cert_cn: build.example.com
   poudriere_cert_key: "{{ poudriere_ssl_private_dir }}/{{ poudriere_cert_cn }}.key"
   poudriere_cert_csr: "{{ poudriere_ssl_dir }}/csr/{{ poudriere_cert_cn }}.csr"
   poudriere_cert_path: "{{ poudriere_ssl_dir }}/certs/{{ poudriere_cert_cn }}.crt"

Optionally, generate the SSL certificate

.. code-block:: console

   shell> ansible-playbook pb.yml -t poudriere_cert -e poudriere_cert=true

Look at the created files, ownership, and permissions

.. literalinclude:: example-cert-tree.txt
   :language: console
   :caption: shell> tree /usr/local/etc/ssl/

.. seealso::

   * Source code :ref:`as_cert.yml`

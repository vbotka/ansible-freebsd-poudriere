.. _task_key:

Generate signing key
^^^^^^^^^^^^^^^^^^^^

.. index:: single: SSL; Tasks/Generate signing key
.. index:: single: poudriere_key; Tasks/Generate signing key
.. index:: single: signing key; Tasks/Generate signing key

The generation of the signing key is enabled by default ::

   poudriere_key: true

By default, the names of the files are ``poudriere-sk.key`` and ``poudriere-sk.crt`` ::

   poudriere_ssl_dir: /usr/local/etc/ssl
   poudriere_ssl_private_dir: /usr/local/etc/ssl/private
   poudriere_conf_pkg_repo_signing_key: "{{ poudriere_ssl_private_dir }}/poudriere-sk.key"
   poudriere_key_crt: "{{ poudriere_ssl_dir }}/crt/poudriere-sk.crt"

Optionally, change the paths and names of the files. For example, ::

   poudriere_cert_cn: build.example.com
   poudriere_conf_pkg_repo_signing_key: "{{ poudriere_ssl_private_dir }}/{{ poudriere_cert_cn }}-sk.key"
   poudriere_key_crt: "{{ poudriere_ssl_dir }}/crt/{{ poudriere_cert_cn }}-sk.crt"

Generate the signing key ::

   shell> ansible-playbook pb.yml -t poudriere_key

Take a look at the created files, ownership, and the permissions

.. literalinclude:: example-key-tree.txt
   :language: sh
   :linenos:
   :emphasize-lines: 1

.. seealso::

   * Source code :ref:`as_key.yml`

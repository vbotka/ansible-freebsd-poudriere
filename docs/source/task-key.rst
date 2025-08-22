.. _task_key:

Generate signing key
^^^^^^^^^^^^^^^^^^^^

.. index:: single: SSL; Tasks/Generate signing key
.. index:: single: poudriere_key; Tasks/Generate signing key
.. index:: single: signing key; Tasks/Generate signing key

By default, generate the signing key

.. code-block:: yaml

   poudriere_key: true

By default, the names of the files are ``poudriere-sk.key`` and ``poudriere-sk.crt``

.. code-block:: yaml

   poudriere_ssl_dir: /usr/local/etc/ssl
   poudriere_ssl_private_dir: /usr/local/etc/ssl/private
   poudriere_conf_pkg_repo_signing_key: "{{ poudriere_ssl_private_dir }}/poudriere-sk.key"
   poudriere_key_crt: "{{ poudriere_ssl_dir }}/crt/poudriere-sk.crt"

Optionally, change the paths and names of the files. For example,

.. code-block:: yaml

   poudriere_cert_cn: build.example.com
   poudriere_conf_pkg_repo_signing_key: "{{ poudriere_ssl_private_dir }}/{{ poudriere_cert_cn }}-sk.key"
   poudriere_key_crt: "{{ poudriere_ssl_dir }}/crt/{{ poudriere_cert_cn }}-sk.crt"

Generate the signing key

.. code-block:: console

   shell> ansible-playbook pb.yml -t poudriere_key

Look at the created files, ownership, and the permissions

.. literalinclude:: example-key-tree.txt
   :language: console
   :caption: shell> tree /usr/local/etc/ssl/

.. seealso::

   * Source code :ref:`as_key.yml`

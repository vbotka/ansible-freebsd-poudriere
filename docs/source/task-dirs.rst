Create SSL directories
^^^^^^^^^^^^^^^^^^^^^^

.. index:: single: SSL; Tasks/Create SSL dirs

The creation of the SSL directories is enabled by default ::

   poudriere_dirs: true
   poudriere_ssl_dir: /usr/local/etc/ssl
   poudriere_ssl_dirs:
     - "{{ poudriere_ssl_dir }}"
     - "{{ poudriere_ssl_dir }}/crt"
     - "{{ poudriere_ssl_dir }}/csr"
   poudriere_ssl_private_dir: /usr/local/etc/ssl/private

Fit the variables to your needs and create the directories ::

   shell> ansible-playbook pb.yml -t poudriere_dirs

.. seealso::

   * Source code :ref:`as_dirs.yml`

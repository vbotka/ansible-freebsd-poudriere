Create SSL directories
^^^^^^^^^^^^^^^^^^^^^^

By default, the creation of the SSL directories is enabled ::

  poudriere_dirs: true
  poudriere_ssl_dir: /usr/local/etc/ssl
  poudriere_ssl_dirs:
    - "{{ poudriere_ssl_dir }}"
    - "{{ poudriere_ssl_dir }}/crt"
    - "{{ poudriere_ssl_dir }}/csr"
  poudriere_ssl_private_dir: /usr/local/etc/ssl/private

Create the directories ::

  shell> ansible-playbook pb.yml -t poudriere_dirs

.. seealso::

   * Source code :ref:`as_dirs.yml`

.. code-block:: bash
   :emphasize-lines: 1

   shell> ansible-playbook pb.yml --list-tags
   
   playbook: pb.yml

   play #1 (build.example.com): build.example.com TAGS: []

      TASK TAGS: [always, poudriere_cert, poudriere_cert_crt,
      poudriere_cert_dirs, poudriere_conf, poudriere_conf_dirs,
      poudriere_conf_file, poudriere_debug, poudriere_make,
      poudriere_options, poudriere_packages, poudriere_pkglists]

.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_cert -e poudriere_cert=true

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Poudriere Debug] ******************************************************
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : cert: Generate private key /usr/local/etc/ssl/private/build.example.com.key]
   changed: [build.example.com]

   TASK [vbotka.freebsd_poudriere : cert: Generate csr /usr/local/etc/ssl/csr/build.example.com.csr] ******
   changed: [build.example.com]

   TASK [vbotka.freebsd_poudriere : cert: Generate crt /usr/local/etc/ssl/certs/build.example.com.crt] ****
   changed: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=1    changed=3    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0


.. literalinclude:: example-cert-tree.txt
   :language: sh
   :linenos:
   :emphasize-lines: 1

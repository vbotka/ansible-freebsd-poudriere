.. code-block:: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_cert -e poudriere_cert=true 
   :linenos:
   :force:

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Cert: Generate private key /usr/local/etc/ssl/private/build.example.com.key]
   changed: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Cert: Generate csr /usr/local/etc/ssl/csr/build.example.com.csr] ******
   changed: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Cert: Generate crt /usr/local/etc/ssl/certs/build.example.com.crt] ****
   changed: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=1    changed=3    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0


.. literalinclude:: example-cert-tree.txt
   :caption: shell> tree /usr/local/etc/ssl/
   :language: console
   :linenos:

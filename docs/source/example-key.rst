.. code-block:: sh
   :linenos:
   :emphasize-lines: 1

   shell> ansible-playbook pb.yml -t poudriere_key

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Key: Generate signing key /usr/local/etc/ssl/private/build.example.com-sk.key]
   changed: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Key: Generate signing crt /usr/local/etc/ssl/crt/build.example.com-sk.crt]
   changed: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=3    changed=2    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0


.. literalinclude:: example-key-tree.txt
   :language: sh
   :linenos:
   :emphasize-lines: 1

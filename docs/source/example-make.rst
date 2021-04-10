.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_make

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Poudriere Debug] ******************************************************
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : conf: Configure /usr/local/etc/poudriere.d/make.conf] *****************
   changed: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=1    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0


.. literalinclude:: example-make.txt
   :language: sh
   :linenos:
   :emphasize-lines: 1

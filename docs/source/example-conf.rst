.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_conf

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Conf: Create directories] *********************************************
   changed: [build.example.com] => (item=/usr/ports/distfiles)

   TASK [vbotka.freebsd_poudriere : Conf: Configure /usr/local/etc/poudriere.conf] ************************
   changed: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=3    changed=2    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0


.. literalinclude:: example-conf.txt
   :language: sh
   :linenos:
   :emphasize-lines: 1

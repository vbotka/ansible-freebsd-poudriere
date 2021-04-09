.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_dirs

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Poudriere Debug] ******************************************************
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : dirs: Create SSL directories] *****************************************
   ok: [build.example.com] => (item=/usr/local/etc/ssl)
   ok: [build.example.com] => (item=/usr/local/etc/ssl/crt)
   ok: [build.example.com] => (item=/usr/local/etc/ssl/csr)

   TASK [vbotka.freebsd_poudriere : dirs: Create SSL directory /usr/local/etc/ssl/private mode 0700] ******
   ok: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=5    changed=3    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

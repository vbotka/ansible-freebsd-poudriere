.. code-block:: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_dirs
   :emphasize-lines: 6,11
   :linenos:
   :force:

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : dirs: Create SSL directories] *****************************************
   ok: [build.example.com] => (item=/usr/local/etc/ssl)
   changed: [build.example.com] => (item=/usr/local/etc/ssl/crt)
   ok: [build.example.com] => (item=/usr/local/etc/ssl/csr)

   TASK [vbotka.freebsd_poudriere : dirs: Create SSL directory /usr/local/etc/ssl/private mode=0700] ******
   ok: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=3    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

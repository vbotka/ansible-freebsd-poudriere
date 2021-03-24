.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_conf

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Poudriere Debug] ******************************************************
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : conf: Create directories] *********************************************
   ok: [build.example.com] => (item=/usr/ports/distfiles)

   TASK [vbotka.freebsd_poudriere : conf: Configure /usr/local/etc/poudriere.conf] ************************
   changed: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=3    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0


.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   shell> cat /usr/local/etc/poudriere.conf
   # Ansible managed 

   ZPOOL=zroot
   NO_ZFS=no
   ZROOTFS=/poudriere
   FREEBSD_HOST=https://download.freebsd.org
   RESOLV_CONF=/etc/resolv.conf
   BASEFS=/usr/local/poudriere
   POUDRIERE_DATA=/usr/local/poudriere/data
   USE_PORTLINT=no
   USE_TMPFS=no
   DISTFILES_CACHE=/usr/ports/distfiles
   PKG_REPO_SIGNING_KEY=/usr/local/etc/ssl/private/build.example.com.key
   URL_BASE=http://build.example.com/
   CHECK_CHANGED_OPTIONS=verbose
   CHECK_CHANGED_DEPS=yes

   # EOF

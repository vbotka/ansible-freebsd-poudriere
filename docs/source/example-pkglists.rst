.. code-block:: sh
   :emphasize-lines: 1,22-23,37-39
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_pkglists

   PLAY [build.example.com] **********************************************************************************************

   TASK [Gathering Facts] ************************************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Poudriere Debug] *********************************************************************
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : pkglists: Create list of packages] ***************************************************
   included: /export/home/vlado.config/.ansible/roles/vbotka.freebsd_poudriere/tasks/pkglist.yml for build.example.com

   TASK [vbotka.freebsd_poudriere : conf: Create list _pkg_dict] *********************************************************
   ok: [build.example.com] => (item=minimal)
   ok: [build.example.com] => (item=ansible)

   TASK [vbotka.freebsd_poudriere : conf: Debug _pkg_dict] ***************************************************************
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : conf: Create directories /usr/local/etc/poudriere.d/pkglist_amd64] *******************
   changed: [build.example.com] => (item=/usr/local/etc/poudriere.d/pkglist_amd64)
   changed: [build.example.com] => (item=/usr/local/etc/poudriere.d/pkglist_amd64.disabled)

   TASK [vbotka.freebsd_poudriere : conf: Remove lists of packages from /usr/local/etc/poudriere.d/pkglist_amd64] ********
   skipping: [build.example.com] => (item=minimal) 
   skipping: [build.example.com] => (item=ansible) 

   TASK [vbotka.freebsd_poudriere : conf: Create lists of packages in /usr/local/etc/poudriere.d/pkglist_amd64.disabled] *
   skipping: [build.example.com] => (item=minimal) 
   skipping: [build.example.com] => (item=ansible) 

   TASK [vbotka.freebsd_poudriere : conf: Remove lists of packages from /usr/local/etc/poudriere.d/pkglist_amd64.disabled]
   ok: [build.example.com] => (item=minimal)
   ok: [build.example.com] => (item=ansible)

   TASK [vbotka.freebsd_poudriere : conf: Create lists of packages in /usr/local/etc/poudriere.d/pkglist_amd64] **********
   changed: [build.example.com] => (item=minimal)
   changed: [build.example.com] => (item=ansible)

   PLAY RECAP ************************************************************************************************************
   build.example.com: ok=6    changed=2    unreachable=0    failed=0    skipped=4    rescued=0    ignored=0


.. code-block:: sh
   :emphasize-lines: 1,8,13
   :linenos:

   shell> tree /usr/local/etc/poudriere.d/
   /usr/local/etc/poudriere.d/
   |-- pkglist_amd64
   |   |-- ansible
   |   `-- minimal
   `-- pkglist_amd64.disabled

   shell> cat /usr/local/etc/poudriere.d/pkglist_amd64/ansible 
   sysutils/ansible
   sysutils/py-ansible-lint
   sysutils/py-ansible-runner

   shell> cat /usr/local/etc/poudriere.d/pkglist_amd64/minimal 
   shells/bash
   devel/git
   archivers/gtar
   ports-mgmt/pkg
   ports-mgmt/portmaster
   ports-mgmt/portupgrade
   net/rsync
   ftp/wget

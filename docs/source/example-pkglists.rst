.. code-block:: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_pkglists
   :emphasize-lines: 15-17,19-21
   :linenos:
   :force:

   PLAY [build.example.com] ********************************************************************************************

   TASK [Gathering Facts] **********************************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Pkglists: Create list of packages] *************************************************
   included: /home/admin/.ansible/roles/vbotka.freebsd_poudriere/tasks/pkglist.yml for build.example.com => (item=amd64)

   TASK [vbotka.freebsd_poudriere : Pkglist: Set variables for amd64] **************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Pkglist: Debug variables poudriere_debug=False] ************************************
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Pkglist: Create directories] *******************************************************
   changed: [build.example.com] => (item=/usr/local/etc/poudriere.d/pkglist/amd64)
   changed: [build.example.com] => (item=/usr/local/etc/poudriere.d/pkglist/amd64.enabled)

   TASK [vbotka.freebsd_poudriere : Pkglist: Create lists of packages in /usr/local/etc/poudriere.d/pkglist/amd64] *****
   changed: [build.example.com] => (item=minimal)
   changed: [build.example.com] => (item=ansible)

   TASK [vbotka.freebsd_poudriere : Pkglist: Remove not enabled lists from /usr/local/etc/poudriere.d/pkglist/amd64.enabled] ***
   ok: [build.example.com] => (item=minimal)
   ok: [build.example.com] => (item=ansible)

   TASK [vbotka.freebsd_poudriere : Pkglist: Link enabled lists to /usr/local/etc/poudriere.d/pkglist/amd64.enabled] ***
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Pkglist: Create lists of all packages] *********************************************
   skipping: [build.example.com] => (item=/usr/local/etc/poudriere.d/pkglist/amd64/All) 
   skipping: [build.example.com] => (item=/usr/local/etc/poudriere.d/pkglist/amd64.enabled/All) 
   skipping: [build.example.com]

   PLAY RECAP **********************************************************************************************************
   build.example.com: ok=6    changed=2    unreachable=0    failed=0    skipped=3    rescued=0    ignored=0


.. code-block:: console
   :caption: shell> tree /usr/local/etc/poudriere.conf
   :linenos:

   /usr/local/etc/poudriere.d/pkglist/
   ├── amd64
   │   ├── ansible
   │   └── minimal
   └── amd64.enabled


.. code-block:: console
   :caption: /usr/local/etc/poudriere.d/pkglist/amd64/ansible
   :linenos:

   sysutils/ansible
   sysutils/py-ansible-lint
   sysutils/py-ansible-runner


.. code-block:: console
   :caption: /usr/local/etc/poudriere.d/pkglist/amd64/minimal
   :linenos:

   shells/bash
   devel/git
   archivers/gtar
   ports-mgmt/pkg
   ports-mgmt/portmaster
   ports-mgmt/portupgrade
   net/rsync
   ftp/wget

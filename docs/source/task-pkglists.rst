Create package lists
^^^^^^^^^^^^^^^^^^^^

.. index:: single: package lists; Tasks/Create package lists
.. index:: single: poudriere_pkglists; Tasks/Create package lists

Quoting from `man(8) poudriere-bulk`_ ::

   -f file      Absolute path to a file which contains the list of ports to
                build.  Ports must be specified in the form category/port
                and shell-style comments are allowed.  Multiple -f file
                arguments may be specified at once.

.. note:: In this role, the term *package lists* is used for the lists of ports in the form
          category/port.

The creation of the package lists is enabled by default ::

   poudriere_pkglists: true

No architecture is selected by default ::

   poudriere_pkg_arch: []

Set the required architectures list the packages will be built for. For example, ::

   poudriere_pkg_arch: [amd64]

For the selected architectures, set the lists of the dictionaries in the variables
``pkg_dict_*.yml``. For example, ::

   pkg_dict_amd64:
     - pkglist: minimal
       packages:
         - shells/bash
         - devel/git@default
         - archivers/gtar
         - ports-mgmt/pkg
         - ports-mgmt/portmaster
         - ports-mgmt/portupgrade
         - net/rsync
         - ftp/wget
     - pkglist: ansible
       packages:
         - sysutils/ansible
         - sysutils/py-ansible-lint
         - sysutils/py-ansible-runner

Optionally, link the enabled package lists in the directory *pkglist/amd64.enabled* ::

   pkglist_enable_amd64:
     - ansible
     - minimal

Optionally, create files *All* including all package lists in the directory ::

   poudriere_pkglist_all: true

Create the package lists files ::

   shell> ansible-playbook pb.yml -t poudriere_pkglists

.. note:: In this role, the term *package lists* is also used for the files keeping the lists of
          ports in the form *category/port* aka *pkg-origin*.

Take a took at the created files ::

   shell> tree /usr/local/etc/poudriere.d/pkglist
   /usr/local/etc/poudriere.d/pkglist
   ├── amd64
   │   ├── All
   │   ├── ansible
   │   └── minimal
   └── amd64.enabled
       ├── All
       ├── ansible -> /usr/local/etc/poudriere.d/pkglist/amd64/ansible
       └── minimal -> /usr/local/etc/poudriere.d/pkglist/amd64/minimal

   shell> cat /usr/local/etc/poudriere.d/pkglist/amd64/ansible
   sysutils/ansible
   sysutils/py-ansible-lint
   sysutils/py-ansible-runner

   shell> cat /usr/local/etc/poudriere.d/pkglist/amd64/minimal
   shells/bash
   devel/git@default
   archivers/gtar
   ports-mgmt/pkg
   ports-mgmt/portmaster
   ports-mgmt/portupgrade
   net/rsync
   ftp/wget

The enablement of the lists in the directory *amd64.enabled* is not mandatory. It's for your
convenience only. See various strategies how to build the packages in the section
:ref:`ug_build_packages`.

.. seealso:: The default lists of the dictionaries in the role `vbotka.freebsd.postinstall`_

.. _`man(8) poudriere-bulk`: https://www.freebsd.org/cgi/man.cgi?query=poudriere-bulk&sektion=8&manpath=freebsd-release-ports
.. _`vbotka.freebsd.postinstall`: https://github.com/vbotka/ansible-freebsd-postinstall/tree/master/defaults/main

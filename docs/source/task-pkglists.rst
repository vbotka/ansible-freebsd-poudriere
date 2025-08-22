Create package lists
^^^^^^^^^^^^^^^^^^^^

.. index:: single: package lists; Tasks/Create package lists
.. index:: single: poudriere_pkglists; Tasks/Create package lists

Quoting from `man(8) poudriere-bulk`_ ::

   -f file      Absolute path to a file which contains the list of ports to
                build.  Ports must be specified in the form category/port
                and shell-style comments are allowed.  Multiple -f file
                arguments may be specified at once.

.. note:: In this role, the term ``package lists`` is used for the lists of ports in the form
          ``category/port``.

By default, create the package lists

.. code-block:: yaml

   poudriere_pkglists: true

No architecture is selected by default

.. code-block:: yaml

   poudriere_pkg_arch: []

Set the required list of architectures for which the packages will be built. For example,

.. code-block:: yaml

   poudriere_pkg_arch: [amd64]

For the selected architectures, set the lists of the dictionaries in the variables
``pkg_dict_*.yml``. For example,

.. code-block:: yaml

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

Optionally, link the enabled package lists in the directory ``pkglist/amd64.enabled``

.. code-block:: yaml

   pkglist_enable_amd64:
     - ansible
     - minimal

Optionally, create files ``All`` including all package lists in the directory

.. code-block:: yaml

   poudriere_pkglist_all: true

Create the package lists files

.. code-block:: console

   shell> ansible-playbook pb.yml -t poudriere_pkglists

.. note:: In this role, the term ``package lists`` is also used for the files keeping the lists of
          ports in the form ``category/port`` aka ``pkg-origin``.

Look at the created files

.. code-block:: console
   :caption: shell> tree /usr/local/etc/poudriere.d/pkglist

   /usr/local/etc/poudriere.d/pkglist
   ├── amd64
   │   ├── All
   │   ├── ansible
   │   └── minimal
   └── amd64.enabled
       ├── All
       ├── ansible -> /usr/local/etc/poudriere.d/pkglist/amd64/ansible
       └── minimal -> /usr/local/etc/poudriere.d/pkglist/amd64/minimal

.. code-block:: console
   :caption: /usr/local/etc/poudriere.d/pkglist/amd64/ansible

   sysutils/ansible
   sysutils/py-ansible-lint
   sysutils/py-ansible-runner

.. code-block:: console
   :caption: /usr/local/etc/poudriere.d/pkglist/amd64/minimal

   shells/bash
   devel/git@default
   archivers/gtar
   ports-mgmt/pkg
   ports-mgmt/portmaster
   ports-mgmt/portupgrade
   net/rsync
   ftp/wget

The enablement of the lists in the directory ``amd64.enabled*`` is not mandatory. It's for your
convenience only. See various strategies how to build the packages in the section
:ref:`ug_build_packages`.

.. seealso:: The default lists of the dictionaries in the role `vbotka.freebsd.postinstall`_

.. _man(8) poudriere-bulk: https://www.freebsd.org/cgi/man.cgi?query=poudriere-bulk&sektion=8&manpath=freebsd-release-ports
.. _vbotka.freebsd.postinstall: https://github.com/vbotka/ansible-freebsd-postinstall/tree/master/defaults/main

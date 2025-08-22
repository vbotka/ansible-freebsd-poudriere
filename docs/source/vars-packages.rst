Package lists
=============

The below variables are used to create lists of packages

:pkg_dict_{{ pkg_arch }}: The package lists.
:pkglist_enable_{{ pkg_arch }}: The list of enabled package lists.
:poudriere_pkglist_all: Create the files ``All`` that keep packages
			from all lists in a directory.

For example,

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

   pkglist_enable_amd64:
     - ansible
     - minimal

   poudriere_pkglist_all: true

will result in the files

.. code-block:: console
   :caption: shell> tree /usr/local/etc/poudriere.d/pkglist/

   /usr/local/etc/poudriere.d/pkglist/
   ├── amd64
   │   ├── All
   │   ├── ansible
   │   └── minimal
   └── amd64.enabled
       ├── All
       ├── ansible -> /usr/local/etc/poudriere.d/pkglist/amd64/ansible
       └── minimal -> /usr/local/etc/poudriere.d/pkglist/amd64/minimal

.. seealso::

   The variables ``pkdict_*.yml`` in the directory `defaults/main`_ of the role `vbotka.freebsd_postinstall`_.


.. _defaults/main: https://github.com/vbotka/ansible-freebsd-postinstall/tree/master/defaults/main
.. _vbotka.freebsd_postinstall: https://galaxy.ansible.com/ui/standalone/roles/vbotka/freebsd_postinstall/

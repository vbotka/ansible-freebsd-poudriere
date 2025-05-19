Package lists
=============

The below variables are used to create lists of packages

:pkg_dict_{{ pkg_arch }}: The package lists.
:pkglist_enable_{{ pkg_arch }}: The list of enabled package lists.
:poudriere_pkglist_all: Create the files ``All`` that keep packages
                        from all lists in a directory.

For example, ::

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

will result in the files ::

   shell> tree /usr/local/etc/poudriere.d/pkglist/
   /usr/local/etc/poudriere.d/pkglist/
   ├── amd64
   │   ├── All
   │   ├── ansible
   │   └── minimal
   └── amd64.enabled
       ├── All
       ├── ansible -> /usr/local/etc/poudriere.d/pkglist/amd64/ansible
       └── minimal -> /usr/local/etc/poudriere.d/pkglist/amd64/minimal

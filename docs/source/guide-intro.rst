.. _ug_introduction:

Introduction
============

Poudriere is a BSD-licensed utility for creating and testing FreeBSD
packages.

* Ansible role: `vbotka.freebsd_poudriere`_
* Supported systems: `FreeBSD`_
* Required collections:

  * `community.general`_
  * `community.crypto`_

| Feel free to `share your feedback and report issues`_
| `Contributions are welcome`_

.. seealso::

   * FreeBSD Handbook `4.6. Building Packages with Poudriere`_
   * FreeBSD Porter's Handbook `10.7. Poudriere`_
   * FreeBSD Wiki `Poudriere - Getting Started`_
   * DO Tutorial `How To Set Up a Poudriere Build System to Create Packages for your FreeBSD Servers`_

Collection vbotka.freebsd
-------------------------

This role role is included in the collection `vbotka.freebsd`_. See the examples:

* `Build packages`_
* `Configure Apache server`_

Package lists
--------------

The utility `poudriere`_ provides the option *-f* to "*Build ports listed in the file*". Ports must
be specified in the form of “category/port”. The utility `pkg`_ uses the mnemonics "pkg-origin" for
this form. In this role, we use lists of “category/port”, or "pkg-origin". For example, the below
variable (list of dictionaries comprises the lists of "pkg-origin")

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

will result in the files

.. code-block:: console

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

The term **package lists** is used both for the variables and the resulting files in this role.

.. _share your feedback and report issues: https://github.com/vbotka/ansible-freebsd-poudriere/issues
.. _Contributions are welcome: https://github.com/firstcontributions/first-contributions

.. _vbotka.freebsd: https://galaxy.ansible.com/ui/repo/published/vbotka/freebsd/
.. _vbotka.freebsd_poudriere: https://galaxy.ansible.com/vbotka/freebsd_poudriere/
.. _vbotka.freebsd.poudriere: https://galaxy.ansible.com/ui/repo/published/vbotka/freebsd/content/role/poudriere/
.. _community.general: https://galaxy.ansible.com/ui/repo/published/community/general/
.. _community.crypto: https://galaxy.ansible.com/ui/repo/published/community/crypto/

.. _FreeBSD: https://www.freebsd.org/releases/
.. _4.6. Building Packages with Poudriere: https://docs.freebsd.org/en_US.ISO8859-1/books/handbook/ports-poudriere.html
.. _10.7. Poudriere: https://docs.freebsd.org/en/books/porters-handbook/testing#testing-poudriere
.. _Poudriere - Getting Started: https://wiki.freebsd.org/VladimirKrstulja/Guides/Poudriere
.. _How To Set Up a Poudriere Build System to Create Packages for your FreeBSD Servers: https://www.digitalocean.com/community/tutorials/how-to-set-up-a-poudriere-build-system-to-create-packages-for-your-freebsd-servers

.. _poudriere: https://man.freebsd.org/cgi/man.cgi?query=poudriere-bulk
.. _pkg: https://man.freebsd.org/cgi/man.cgi?query=pkg-upgrade

.. _Build packages: https://ansible-collection-freebsd.readthedocs.io/en/latest/examples/390/example.html#index-0
.. _Configure Apache server: https://ansible-collection-freebsd.readthedocs.io/en/latest/examples/423/example.html#index-0

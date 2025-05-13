.. _ug_introduction:

Introduction
============

Poudriere is a BSD-licensed utility for creating and testing FreeBSD
packages.

* Ansible role: `vbotka.freebsd_poudriere`_
* Supported systems: `FreeBSD`_
* Requirements:

  * `community.general`_
  * `community.crypto`_

| Feel free to `share your feedback and report issues`_
| `Contributions are welcome`_

.. seealso::

   * FreeBSD Handbook `4.6. Building Packages with Poudriere`_
   * FreeBSD Porter's Handbook `10.7. Poudriere`_
   * FreeBSD Wiki `Poudriere: Getting Started`_
   * DO Tutorial `How To Set Up a Poudriere Build System to Create Packages for your FreeBSD Servers`_

Packages lists
--------------

The utility `poudriere`_ provides the option *-f* to "*Build ports listed in the file*". Ports must
be specified in the form of “category/port”. The utility `pkg`_ uses the mnemonics "pkg-origin" for
this form. In this role, we use lists of “category/port”, or "pkg-origin". For example, the below
variable (list of dictionaries comprises the lists of "pkg-origin") ::

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

The term **packages lists** is used both for the variables and the resulting files in this role.

.. _share your feedback and report issues: https://github.com/vbotka/ansible-freebsd-poudriere/issues
.. _Contributions are welcome: https://github.com/firstcontributions/first-contributions

.. _`vbotka.freebsd_poudriere`: https://galaxy.ansible.com/vbotka/freebsd_poudriere
.. _`community.general`: https://galaxy.ansible.com/ui/repo/published/community/general/
.. _`community.crypto`: https://galaxy.ansible.com/ui/repo/published/community/crypto/

.. _`FreeBSD`: https://www.freebsd.org/releases/
.. _`4.6. Building Packages with Poudriere`: https://docs.freebsd.org/en_US.ISO8859-1/books/handbook/ports-poudriere.html
.. _`10.7. Poudriere`: https://docs.freebsd.org/en/books/porters-handbook/testing#testing-poudriere
.. _`Poudriere: Getting Started`: https://wiki.freebsd.org/VladimirKrstulja/Guides/Poudriere
.. _`How To Set Up a Poudriere Build System to Create Packages for your FreeBSD Servers`: https://www.digitalocean.com/community/tutorials/how-to-set-up-a-poudriere-build-system-to-create-packages-for-your-freebsd-servers

.. _`poudriere`: https://man.freebsd.org/cgi/man.cgi?query=poudriere-bulk
.. _`pkg`: https://man.freebsd.org/cgi/man.cgi?query=pkg-upgrade

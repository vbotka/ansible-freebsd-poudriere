.. code-block:: yaml
   :caption: host_vars/build.example.com/pkg_dict.yml
   :emphasize-lines: 2
   :linenos:

   ---
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

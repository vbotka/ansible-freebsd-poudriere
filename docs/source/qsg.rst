.. _qg:

Quick start guide
*****************

For the users who want to try the role quickly, this guide provides an example of how to install,
configure and run `Poudriere
<https://docs.freebsd.org/en/books/porters-handbook/testing-poudriere.html>`_


* Install the role ``vbotka.freebsd_poudriere`` ::

    shell> ansible-galaxy install vbotka.freebsd_poudriere


* Create the playbook ``pb.yml`` for single host build.example.com (2)

.. code-block:: bash
   :emphasize-lines: 3
   :linenos:

   shell> cat pb.yml
   ---
   - hosts: build.example.com
     become: true
     roles:
       - vbotka.freebsd_poudriere


* Customized variables

.. code-block:: bash
   :emphasize-lines: 3
   :linenos:

   shell> cat host_vars/build.example.com/poudriere.yml
   ---
   poudriere_conf_URL_BASE: build.example.com
   poudriere_cert_CN: build.example.com
   poudriere_conf_PKG_REPO_SIGNING_KEY: "{{ poudriere_ssl_dir }}/private/{{ poudriere_cert_CN }}.key"
   poudriere_conf_NO_ZFS: "no"
   poudriere_conf_ZPOOL: zroot
   poudriere_conf_USE_TMPFS: "no"
   poudriere_pkg_arch: [amd64]
   poudriere_csr_path: "{{ poudriere_ssl_dir }}/csr/{{ poudriere_cert_CN }}.csr"
   poudriere_cert_path: "{{ poudriere_ssl_dir }}/crt/{{ poudriere_cert_CN }}.crt"


* Create lists of the packages

.. code-block:: bash
   :emphasize-lines: 4,14
   :linenos:

   shell> cat host_vars/build.example.com/poudriere.yml
   ---
   pkg_dict_amd64:
     - pkglist: minimal
       packages:
         - shells/bash
         - devel/git
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


* Test syntax ::

    shell> ansible-playbook pb.yml --syntax-check


* See what variables will be included ::

    shell> ansible-playbook pb.yml -t poudriere_debug -e poudriere_debug=true


* Install packages ::

    shell> ansible-playbook pb.yml -t poudriere_packages


* Dry-run, display differences and display variables ::

    shell> ansible-playbook pb.yml -e poudriere_debug=true --check --diff


* If all seems to be right run the playbook ::

    shell> ansible-playbook pb.yml

* If the command above completed without errors Poudriere should have been installed and
  configured. Login into build.example.com and proceed according the `Poudriere documentation <https://docs.freebsd.org/en/books/porters-handbook/testing-poudriere.html>`_ , e.g. ::

   shell> poudriere jail -c -j 12amd64 -v 12.2-RELEASE
   shell> poudriere ports -c -p local
   shell> poudriere bulk -j 12amd64 -p local -z devel \
          -f /usr/local/etc/poudriere.d/pkglist_amd64/minimal


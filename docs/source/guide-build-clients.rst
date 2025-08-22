.. _ug_build_client:

Configure clients
-----------------

See FreeBSD Handbook chapter `Configuring pkg Clients to Use a Poudriere Repository`_.


.. _ug_build_client_repo:

Configure repos
^^^^^^^^^^^^^^^

Log to the clients. For example, ::

   shell> uname -a
   FreeBSD test 14.1-RELEASE FreeBSD 14.1-RELEASE releng/14.1-n267679-10e31f0946d8 GENERIC amd64

and configure the repository. Copy the certificate ``build.example.com-sk.crt`` you created in
:ref:`task_key`

.. code-block:: yaml
   :caption: /usr/local/etc/pkg/repos/build.conf

   build: {
     url: "http://build.example.com/packages/141Ramd64-default-devel",
     mirror_type: "none",
     enabled: yes,
     signature_type: "pubkey",
     pubkey: "/usr/local/etc/ssl/crt/build.example.com-sk.crt"
   }

Disable the official repository

.. code-block:: yaml
   :caption: /usr/local/etc/pkg/repos/freebsd.conf

   FreeBSD: {
       enabled: no
   }

Display the configuration and repo details

.. code-block:: yaml
   :caption: shell> pkg -vv

   ...
   Repositories:
     build: {
       url             : "http://build.example.com/packages/141Ramd64-default-devel",
       enabled         : yes,
       priority        : 0,
       signature_type  : "PUBKEY",
       pubkey          : "/usr/local/etc/ssl/crt/build.example.com-sk.crt"
     }


.. _ug_build_client_repo_local:

Configure local repo
^^^^^^^^^^^^^^^^^^^^

In the localhost use url ``file://`` instead of ``http://``

.. code-block:: yaml
   :caption: /usr/local/etc/pkg/repos/build.conf

   build: {
     url: "file:///usr/local/poudriere/data/packages/141Ramd64-default-devel/",
     mirror_type: "none",
     enabled: yes,
     signature_type: "pubkey",
     pubkey: "/usr/local/etc/ssl/crt/build.example.com-sk.crt"
   }

.. seealso::

  * FreeBSD Handbook `Configuring pkg Clients to Use a Poudriere Repository`_
  * `man pkg(8)`_
  * `man pkg-repo(8)`_
  * `man pkg.conf(5)`_


.. _ug_build_client_repo_ansible:

Configure repos by Ansible
^^^^^^^^^^^^^^^^^^^^^^^^^^

Look at the Ansible role `vbotka.freebsd_packages`_.

Create the configuration data on the controller

.. code-block:: yaml
   :caption: host_vars/test.example.com/packages.yml

   pkg_repos_conf:
     - name: build
       conf:
         - {key: 'url', value: '"http://build.example.com/packages/141Ramd64-default-devel"'}
         - {key: 'mirror_type', value: '"nomirror"'}
         - {key: 'enabled', value: 'yes'}
         - {key: 'signature_type', value: '"pubkey"'}
         - {key: 'pubkey', value: '"/usr/local/etc/ssl/crt/build.example.com-sk.crt"'}
     - name: FreeBSD
       conf:
         - { key: enabled, value: "no" }

and run ``ansible-playbook`` to configure the repos on the remote host ``test.example.com``

.. code-block:: yaml
   :caption: shell> ansible-playbook freebsd-packages.yml -t pkg_conf
   :force:

   TASK [vbotka.freebsd_packages : Conf: Create directories] *******************
   ok: [test.example.com] => (item=/usr/local/etc/pkg)
   ok: [test.example.com] => (item=/usr/local/etc/pkg/repos)

   TASK [vbotka.freebsd_packages : Conf: Configure /usr/local/etc/pkg/repos] ***
   ok: [test.example.com] => (item=build)
   ok: [test.example.com] => (item=FreeBSD)


.. _ug_build_client_install:

Install packages
^^^^^^^^^^^^^^^^

See the FreeBSD Handbook Chapter `Installing and Fetching Packages`_.

Update the pkg database

.. code-block:: console
   :caption: shell> pkg update

   Updating build repository catalogue...
   Fetching meta.conf: 100%    178 B   0.2kB/s    00:01
   Fetching data.pkg: 100%  140 KiB 143.8kB/s    00:01
   Processing entries: 100%
   build repository update completed. 500 packages processed.
   All repositories are up to date.

Display packages info. For example,

.. code-block:: console
   :caption: shell> pkg info | grep pkg

   pkg-1.21.3                    Package manager

Upgrade the package

.. code-block:: console
   :caption: shell> pkg upgrade pkg

   Updating build repository catalogue...
   build repository is up to date.
   All repositories are up to date.
   Checking integrity... done (0 conflicting)
   Your packages are up to date.

.. seealso::

   * Ansible role `vbotka.freebsd_postinstall`_
   * Chapter `Packages`_.


.. _`Configuring pkg Clients to Use a Poudriere Repository`: https://docs.freebsd.org/en/books/handbook/ports/#_configuring_pkg_clients_to_use_a_poudriere_repository
.. _`Installing and Fetching Packages`: https://docs.freebsd.org/en/books/handbook/ports/#pkg-installing-fetching
.. _`Packages`: https://ansible-freebsd-postinstall.readthedocs.io/en/latest/tasks-packages.html
.. _`vbotka.freebsd_packages`: https://galaxy.ansible.com/ui/standalone/roles/vbotka/freebsd_packages/
.. _`vbotka.freebsd_postinstall`: https://galaxy.ansible.com/ui/standalone/roles/vbotka/freebsd_postinstall/
.. _`man pkg(8)`: https://www.freebsd.org/cgi/man.cgi?query=pkg&sektion=&n=1
.. _`man pkg-repo(8)`: https://man.freebsd.org/cgi/man.cgi?query=pkg-repo&sektion=8&n=1
.. _`man pkg.conf(5)`: https://man.freebsd.org/cgi/man.cgi?query=pkg.conf&sektion=5&n=1

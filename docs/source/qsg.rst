.. _qg:

Quick start guide
*****************

For the users who want to try the role quickly, this guide provides an example how to install,
configure and run `Poudriere`_


* Install the role ``vbotka.freebsd_poudriere``

  .. code-block:: console

     shell> ansible-galaxy role install vbotka.freebsd_poudriere

* Install the collections if necessary

  .. code-block:: console

     shell> ansible-galaxy collection install community.crypto
     shell> ansible-galaxy collection install community.general

* Create the playbook ``pb.yml``. For example, with single host ``build.example.com`` (2)

.. literalinclude:: qsg/pb.yml
   :language: yaml
   :caption: pb.yml
   :emphasize-lines: 2
   :linenos:

* Customize variables. Disable the installation of ``packages`` (2). Configure web server
  ``certificate`` (5-8), repository ``signing key`` (17-18) and Poudriere ``parameters
  (21-45)``. Create the list of ``architectures`` for which the packages will be built (48) and
  configure ``make`` (51-57). Fit the configuration to your needs.

.. literalinclude:: qsg/poudriere.yml
   :language: yaml
   :caption: host_vars/build.example.com/poudriere.yml
   :linenos:

* Create the package lists

.. literalinclude:: qsg/pkg_dict.yml
   :language: yaml
   :caption: host_vars/build.example.com/pkg_dict.yml
   :emphasize-lines: 2
   :linenos:

* Test the syntax

  .. code-block:: console

     shell> ansible-playbook pb.yml --syntax-check

     playbook: pb.yml

* Display the included variables. Enable debug ``poudriere_debug=true``

.. literalinclude:: qsg/out-01.txt
   :language: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_debug -e poudriere_debug=true
   :force:
   :linenos:

* Configure ZFS ::

   <TBD>

* Install packages. Enable the installation ``poudriere_install=true``

.. literalinclude:: qsg/out-02.txt
   :language: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_pkg -e poudriere_install=true
   :force:
   :linenos:

* Create directories

.. literalinclude:: qsg/out-03.txt
   :language: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_dirs
   :force:
   :linenos:

* Generate the signing key

.. literalinclude:: qsg/out-04.txt
   :language: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_key
   :force:
   :linenos:

* Generate the certificate for the web server. Enable the generation ``poudriere_cert=true``

.. literalinclude:: qsg/out-05.txt
   :language: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_cert -e poudriere_cert=true
   :force:
   :linenos:

.. literalinclude:: qsg/out-06.txt
   :language: console
   :caption: shell> ssh admin@$build_example_com sudo tree /usr/local/etc/ssl/
   :linenos:

* Configure poudriere

.. literalinclude:: qsg/out-07.txt
   :language: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_conf
   :force:
   :linenos:

* Create directories (12), create package lists (16), and link enabled lists (20)

.. literalinclude:: qsg/out-08.txt
   :language: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_pkglists
   :force:
   :linenos:

.. literalinclude:: qsg/out-09.txt
   :language: console
   :caption: shell> ssh admin@$build_example_com tree /usr/local/etc/poudriere.d/pkglist/
   :linenos:

.. literalinclude:: qsg/out-10.txt
   :language: console
   :caption: /usr/local/etc/poudriere.d/pkglist/amd64/ansible
   :linenos:

.. literalinclude:: qsg/out-11.txt
   :language: console
   :caption: /usr/local/etc/poudriere.d/pkglist/amd64/minimal
   :linenos:

* Configure make

.. literalinclude:: qsg/out-12.txt
   :language: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_make
   :force:
   :linenos:

* The role is idempotent. At this point, Poudriere is installed, configured, and ready to build
  packages. There should be no changes reported when the playbook is run repeatedly with the same
  data ::

    shell> ansible-playbook pb.yml

* Build the packages. Login into the host ``build.example.com`` and proceed according the `Poudriere
  documentation`_. For example,

.. include:: example-bulk.rst

.. _Poudriere: https://docs.freebsd.org/en/books/porters-handbook/testing-poudriere.html
.. _Poudriere documentation: https://docs.freebsd.org/en/books/porters-handbook/testing-poudriere.html

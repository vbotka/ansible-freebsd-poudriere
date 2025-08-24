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

.. include:: example-playbook.rst

* Customize variables. Disable the installation of ``packages`` (2). Configure web server
  ``certificate`` (5-8), repository ``signing key`` (17-18) and Poudriere ``parameters
  (21-45)``. Create the list of ``architectures`` for which the packages will be built (48) and
  configure ``make`` (51-57). Fit the configuration to your needs.

.. include:: example-vars-poudriere.rst

* Create the package lists

.. include:: example-vars-pkgdict.rst

* Test the syntax

  .. code-block:: console

     shell> ansible-playbook pb.yml --syntax-check

     playbook: pb.yml

* Display the included variables. Enable debug ``poudriere_debug=true``

.. include:: example-debug.rst

* Configure ZFS ::

   <TBD>

* Install packages. Enable the installation ``poudriere_install=true``

.. include:: example-packages.rst

* Create directories

.. include:: example-dirs.rst

* Generate the signing key

.. include:: example-key.rst

* Generate the certificate for the web server. Enable the generation ``poudriere_cert=true``

.. include:: example-cert.rst

* Configure poudriere

.. include:: example-conf.rst

* Create directories (15-17) and create the package lists (19-21)

.. include:: example-pkglists.rst

* Configure make

.. include:: example-make.rst

* The role is idempotent. At this point, Poudriere is installed, configured, and ready to build
  packages. There should be no changes reported when the playbook is run repeatedly with the same
  data ::

   shell> ansible-playbook pb.yml

* Build the packages. Login into the host ``build.example.com`` and proceed according the `Poudriere
  documentation`_. For example,

.. include:: example-bulk.rst

.. _Poudriere: https://docs.freebsd.org/en/books/porters-handbook/testing-poudriere.html
.. _Poudriere documentation: https://docs.freebsd.org/en/books/porters-handbook/testing-poudriere.html

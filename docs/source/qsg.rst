.. _qg:

Quick start guide
*****************

For the users who want to try the role quickly, this guide provides an example of how to install,
configure and run `Poudriere
<https://docs.freebsd.org/en/books/porters-handbook/testing-poudriere.html>`_


**Install the role** ``vbotka.freebsd_poudriere`` and the collections ::

    shell> ansible-galaxy role install vbotka.freebsd_poudriere
    shell> ansible-galaxy collection install community.crypto
    shell> ansible-galaxy collection install community.general


**Create the playbook** ``pb.yml`` for single host build.example.com (3)

.. include:: example-playbook.rst

**Customize variables.** Disable the installation of packages (3). Configure web-server certificate
(6-9), repository signing key (12-13) and parameters of Poudriere (16-40). Create the list of
architectures the packages will be built for (43) and configure make (46-52). Fit the configuration
to your needs.

.. include:: example-vars-poudriere.rst

**Create lists of the ports**

.. include:: example-vars-pkgdict.rst

**Test syntax** ::

    shell> ansible-playbook pb.yml --syntax-check

    playbook: pb.yml

**Display the included variables.** Enable debug ``poudriere_debug=true``

.. include:: example-debug.rst

**Configure ZFS** ::

    <TBD>

**Install packages.** Enable the installation ``poudriere_install=true``

.. include:: example-packages.rst

**Create directories**

.. include:: example-dirs.rst

**Generate signing key**

.. include:: example-key.rst

**Generate certificate for the web server.** Enable the generation ``poudriere_cert=true`` (default=false)

.. include:: example-cert.rst

**Configure poudriere**

.. include:: example-conf.rst

**Create directories** (22-23) and **create the lists of the ports** (37-39)

.. include:: example-pkglists.rst

**Configure make**

.. include:: example-make.rst

**The role is idempotent.** At this point, Poudriere is installed, configured and ready to build the
packages. There should be no changes reported when the playbook is run repeatedly with the same data
::

    shell> ansible-playbook pb.yml

**Build the packages.** Login into the host build.example.com and proceed according the `Poudriere documentation <https://docs.freebsd.org/en/books/porters-handbook/testing-poudriere.html>`_ ,
e.g. ::

   shell> poudriere jail -c -j 12amd64 -v 12.2-RELEASE
   shell> poudriere ports -c -p local
   shell> poudriere bulk -j 12amd64 -p local -z devel \
          -f /usr/local/etc/poudriere.d/pkglist_amd64/minimal

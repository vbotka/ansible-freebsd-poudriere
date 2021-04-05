Install packages or ports
^^^^^^^^^^^^^^^^^^^^^^^^^

Install FreeBSD packages or ports needed by Poudriere ``poudriere_packages`` and also packages
needed to generate the certificate ``poudriere_packages_cert``.

By default, the installation is enabled ::

  poudriere_install: true

By default, install packages ::

  freebsd_install_method: packages

If you decide to install from ports set ::

  freebsd_install_method: ports

To install prebuild packages set ::

  freebsd_use_packages: true

or build the packages from the ports first ::

  freebsd_use_packages: false

Install packages ::

  shell> ansible-playbook pb.yml -t poudriere_packages -e poudriere_install=true

The best practice is disabling the installation to speedup the execution of the playbook ::

  poudriere_install: false

.. seealso::

   * Source code :ref:`as_packages.yml`
   * FreeBSD Handbook `Chapter 4. Installing Applications: Packages and Ports <https://docs.freebsd.org/en_US.ISO8859-1/books/handbook/ports.html>`_

Install packages or ports
^^^^^^^^^^^^^^^^^^^^^^^^^

.. index:: single: poudriere_packages; Tasks/Install packages or ports
.. index:: single: poudriere_packages_cert; Tasks/Install packages or ports

Install FreeBSD packages or ports needed by Poudriere from the list ``poudriere_packages``. Also,
install packages needed to generate the signing key, and the certificate from the list
``poudriere_packages_cert``.

The installation of packages is enabled by default ::

   poudriere_install: true
   freebsd_install_method: packages

If you want to install from ports set ::

   freebsd_install_method: ports

To install pre-build packages, when available, set ::

   freebsd_use_packages: true

, or build the packages from the ports first ::

   freebsd_use_packages: false

Install packages ::

   shell> ansible-playbook pb.yml -t poudriere_pkg -e poudriere_install=true

After the installation, speed up the execution of the playbook. Set ::

   poudriere_install: false

.. seealso::

   * Source code :ref:`as_pkg.yml`
   * FreeBSD Handbook `Chapter 4. Installing Applications: Packages and Ports`_

.. _`Chapter 4. Installing Applications: Packages and Ports`: https://docs.freebsd.org/en_US.ISO8859-1/books/handbook/ports.html

Install packages or ports
^^^^^^^^^^^^^^^^^^^^^^^^^

.. index:: single: poudriere_packages; Tasks/Install packages or ports
.. index:: single: poudriere_packages_cert; Tasks/Install packages or ports

Install FreeBSD packages or ports needed by Poudriere from the list ``poudriere_packages``. Also,
install packages needed to generate the signing key, and the certificate from the list
``poudriere_packages_cert``.

The installation of packages is enabled by default

.. code-block:: yaml

   poudriere_install: true
   freebsd_install_method: packages

If you want to install from ports set

.. code-block:: yaml

   freebsd_install_method: ports

To install pre-build packages, when available, set

.. code-block:: yaml

   freebsd_use_packages: true

, or build the packages from the ports first

.. code-block:: yaml

   freebsd_use_packages: false

Install packages

.. code-block:: console

   shell> ansible-playbook pb.yml -t poudriere_pkg -e poudriere_install=true

After the installation, speed up the execution of the playbook. Set

.. code-block:: yaml

   poudriere_install: false

.. seealso::

   * Source code :ref:`as_pkg.yml`
   * FreeBSD Handbook `Chapter 4. Installing Applications - Packages and Ports`_

.. _Chapter 4. Installing Applications - Packages and Ports: https://docs.freebsd.org/en_US.ISO8859-1/books/handbook/ports.html

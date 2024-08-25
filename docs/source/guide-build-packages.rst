.. _ug_build_packages:

Build the packages
------------------

There are many options how to use the packages lists:

* Build all packages from a directory. For example, ::

   shell> poudriere bulk -j 12arm7 -z devel -f /usr/local/etc/poudriere.d/pkglist/arm/All

* If you didn't create the file *All* create a script and iterate all lists. For example, ::

   #!/bin/sh
   for i in /usr/local/etc/poudriere.d/pkglist/arm/*; do
     poudriere bulk -j 12arm7 -z devel -f ${i}
   done

* You can speedup the process and specify all lists in one command. For example, ::

   #!/bin/sh
   my_dir=/usr/local/etc/poudriere.d/pkglist/arm/
   my_lists=$(find ${my_dir}* | xargs printf " -f %s")
   poudriere bulk -j 12arm7 -z devel ${my_lists}


.. note::

   When web-server is configured the current status should be
   available on-line (see the next section *Export data*). For
   example,

   ``https://build.example.com/logs/bulk/12arm7-local-devel/latest/build.html``


.. seealso::

   * FreeBSD Porter's Handbook `10.7. poudriere`_
   * FreeBSD Porter's Handbook `10.7.3. Creating poudriere Jails`_
   * FreeBSD Porter's Handbook `10.7.5. Setting Up Ports Trees for Use with poudriere`_
   * `man poudriere-bulk`_
   * `FreeBSD Wiki arm64/ports`_
   * `FreeBSD Wiki arm`_


.. toctree::
   :caption: Examples

   guide-build-141-amd64-minimal
   guide-build-141-amd64-all-enabled
   guide-build-12-amd64
   guide-build-12-arm7


.. _`10.7. poudriere`: https://docs.freebsd.org/en/books/porters-handbook/testing/#testing-poudriere
.. _`10.7.3. Creating poudriere Jails`: https://docs.freebsd.org/en/books/porters-handbook/testing/#testing-poudriere-create-jails
.. _`10.7.5. Setting Up Ports Trees for Use with poudriere`: https://docs.freebsd.org/en/books/porters-handbook/testing/#testing-poudriere-ports-tree
.. _`man poudriere-bulk`: https://man.freebsd.org/cgi/man.cgi?query=poudriere-bulk
.. _`FreeBSD Wiki arm64/ports`: https://wiki.freebsd.org/arm64/ports
.. _`FreeBSD Wiki arm`: https://wiki.freebsd.org/arm

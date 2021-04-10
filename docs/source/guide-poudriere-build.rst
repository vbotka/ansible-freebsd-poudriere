.. _ug_build:

Build the packages
------------------

.. toctree::
   :caption: Table of Contents

   guide-poudriere-build-amd64
   guide-poudriere-build-arm7


.. note::

   When web-server is configured (see the next section *Export data*) the current status should be
   available on-line, e.g.
   ``https://build.example.com/logs/bulk/12arm7-local-devel/latest/build.html``

.. seealso::

   * FreeBSD Wiki `arm64/ports <https://wiki.freebsd.org/arm64/ports>`_
   * FreeBSD Wiki `arm <https://wiki.freebsd.org/arm>`_

Batch
^^^^^

Build packages from all lists in the dictionary, e.g. ::

   #!/bin/sh
   for i in /usr/local/etc/poudriere.d/pkglist_arm/*; do
     poudriere bulk -j 12arm7 -p local -z devel -f ${i}
   done

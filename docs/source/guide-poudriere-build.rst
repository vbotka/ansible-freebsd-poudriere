.. _ug_build:

Build the packages
------------------

.. toctree::

   guide-poudriere-build-amd64
   guide-poudriere-build-arm7


.. seealso::

   * FreeBSD Wiki `arm64/ports <https://wiki.freebsd.org/arm64/ports>`_
   * FreeBSD Wiki `arm <https://wiki.freebsd.org/arm>`_

Batch
^^^^^

Build packages from all lists in the dictionary, e.g. ::

   #!/bin/sh
   for i in /usr/local/etc/poudriere.d/pkglist_amd64/*; do
     poudriere bulk -j 11amd64 -p local -z setname -f ${i};
   done

.. _ug_build_141amd64_all_enabled:

Build 14.1 amd64 all enabled lists
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Create jail ::

   shell> poudriere jail -c -j 141Ramd64 -v 14.1-RELEASE -a amd64

Create ports tree ::
    
   shell> poudriere ports -c -m git+https -B main

Build ports listed in the file ``All`` ::

   shell> poudriere bulk -j 141Ramd64 -z devel -f /usr/local/etc/poudriere.d/pkglist/amd64.enabled/All

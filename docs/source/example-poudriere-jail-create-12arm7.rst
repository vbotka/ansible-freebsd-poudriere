.. _ug_example_jail_create_12arm7:

jail create 12arm7
""""""""""""""""""

Use the mounted image */zroot/poudriere/jails/12arm7*. Create the jail ::

  shell> poudriere jail -c -m null -j 12arm7 -v 12.2-RELEASE -a armv7 -M /zroot/poudriere/jails/12arm7

,or update it if it already exists ::

  shell> poudriere jail -u -m null -j 12arm7 -v 12.2-RELEASE -a armv7 -M /zroot/poudriere/jails/12arm7


.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   [root@build /usr/home/admin]# poudriere jail -c -m null -j 12arm7 -v 12.2-RELEASE -a armv7 -M /zroot/poudriere/jails/12arm7
   [00:00:00] Cross-building ports for armv7 on amd64 requires QEMU
   [00:00:00] Recording filesystem state for clean... done
   [00:00:00] Jail 12arm7 12.2-RELEASE armv7 is ready to be used

.. _ug_example_poudriere_options_12arm7:

Configure ports' options for jail 12arm7
----------------------------------------

If necessary, manually change options and dependencies for the specified ports ::

  [root@build /usr/home/admin]# poudriere options -j 12arm7 -p local -z devel -f /usr/local/etc/poudriere.d/pkglist_arm/minimal

  <TBD>

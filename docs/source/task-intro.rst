Introduction
^^^^^^^^^^^^

The groups of tasks stored in separate files, listed below in the order of the execution, comprise:

:debug: Display values of the variables. By default disabled (poudriere_debug: false)
:sanity: Test sanity. By default disabled (poudriere_sanity: false)
:pkg: Install packages or ports. By default enabled (poudriere_install: true)
:dirs: Create SSL directories. By default enabled (poudriere_dirs: true)
:key: Create signing key. By default enabled (poudriere_key: true)
:cert: Generate SSL certificate for the web server. By default disabled (poudriere_cert: false)
:conf: Configure Poudriere. By default enabled (poudriere_conf: true)
:pkglists: Create lists of ports. By default enabled (poudriere_pkglists: true)
:options: Create options file for each jail. Not implemented yet. Disabled (poudriere_options: false)
:make: Customize make. By default enabled (poudriere_make: true)

The following sections describe how to run each group of tasks separately. This can be useful to
debug and tune the installation and configuration. In each step, you can dry-run the group of tasks
with options "*--check --diff*" and show the differences. If this is what you want run the group of
tasks. When you are sure the configuration is ready run the whole play ::

   shell> ansible-playbook pb.yml

.. seealso::

   * Source code :ref:`as_main.yml`
   * ``man ansible-playbook``

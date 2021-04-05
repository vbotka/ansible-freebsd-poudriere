.. _ug_tasks:

Tasks
-----

The groups of tasks stored in separate files comprise

* Display values of the variables. By default disabled (poudriere_debug: false)
* Install packages or ports. By default enabled (poudriere_install: true)
* Generate SSL certificate. By default disabled (poudriere_cert: false)
* Configure Poudriere. By default enabled (poudriere_conf: true)
* Create lists of ports. By default enabled (poudriere_pkglists: true)
* Configure ports' options. By default disabled (poudriere_options: false)
* Customize make. By default enabled (poudriere_make: true)


.. seealso::

   * Source code :ref:`as_main.yml`

.. note::

   * Feel free to `share your feedback and report issues <https://github.com/vbotka/ansible-freebsd-poudriere/issues>`_

   * `Contributions are welcome <https://github.com/firstcontributions/first-contributions>`_

.. toctree::

   task-packages
   task-cert
   task-conf
   task-pkglist
   task-options
   task-make

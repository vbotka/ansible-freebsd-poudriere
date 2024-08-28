.. _as_tasks:

Tasks
=====

.. _as_main.yml:

main.yml
--------

Synopsis: Main task.


Import tasks if enabled.


[`tasks/main.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/main.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/main.yml
    :language: Yaml
    :emphasize-lines: 1,2
    :linenos:





.. _as_debug.yml:

debug.yml
---------

Synopsis: Display values of the variables.


By default disabled ``poudriere_debug: false``


[`tasks/debug.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/debug.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/debug.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>




.. _as_pkg.yml:

pkg.yml
-------

Synopsis: Install packages or ports.


By default enabled ``poudriere_install: true``


[`tasks/pkg.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/pkg.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/pkg.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>




.. _as_dirs.yml:

dirs.yml
--------

Synopsis: Create SSL directories.


By default enabled ``poudriere_dirs: true``


[`tasks/dirs.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/dirs.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/dirs.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>




.. _as_key.yml:

key.yml
-------

Synopsis: Create signing key.


By default enabled ``poudriere_key: true``


[`tasks/key.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/key.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/key.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>




.. _as_cert.yml:

cert.yml
--------

Synopsis: Generate SSL certificate for the web server.


By default disabled ``poudriere_cert: false``


[`tasks/cert.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/cert.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/cert.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>




.. _as_conf.yml:

conf.yml
--------

Synopsis: Configure Poudriere.


By default enabled ``poudriere_conf: true``


[`tasks/conf.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/conf.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/conf.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>




.. _as_pkglists.yml:

pkglists.yml
------------

Synopsis: Create packages lists.


By default enabled ``poudriere_pkglists: true``


[`tasks/pkglists.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/pkglists.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/pkglists.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>




.. _as_pkglist.yml:

pkglist.yml
-----------

Synopsis: Maintain packages lists for a particular architecture.


These lists will be used by *poudriere*. Quoting *man poudriere*: *"Launch the bulk build. At minimum the jail and list of packages to build must be specified."*

For example, ::

   shell> poudriere bulk -j 141Ramd64 -f /usr/local/etc/poudriere.d/pkglist/amd64/minimal


[`tasks/pkglist.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/pkglist.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/pkglist.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>




.. _as_options.yml:

options.yml
-----------

Synopsis: Create options file for each jail


Not implemented yes. Disabled ``poudriere_options: false``


[`tasks/options.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/options.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/options.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>




.. _as_make.yml:

make.yml
--------

Synopsis: Customize make.


By default enabled ``poudriere_make: true``


[`tasks/make.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/tasks/make.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../tasks/make.yml
    :language: Yaml
    :emphasize-lines: 2
    :linenos:

.. seealso::
   * <TBD>





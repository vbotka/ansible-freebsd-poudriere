.. _ug_tags:

Tags
----

The :index:`tags` provide the user with a very useful tool to run selected tasks of the role. To see
what tags are available list the tags of the role with the command

.. include:: tags-list.rst

For example, display the list of the variables and their values with the tag ``poudriere_debug`` (when the
debug is enabled ``poudriere_debug: true``)

.. code-block:: console
   :emphasize-lines: 1

    shell> ansible-playbook playbook.yml -t poudriere_debug

See what packages will be installed

.. code-block:: console
   :emphasize-lines: 1

    shell> ansible-playbook playbook.yml -t poudriere_packages --check

Install packages and exit the play

.. code-block:: console
   :emphasize-lines: 1

    shell> ansible-playbook playbook.yml -t poudriere_packages

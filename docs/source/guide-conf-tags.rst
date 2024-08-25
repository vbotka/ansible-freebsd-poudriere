.. _ug_tags:

Tags
----

The :index:`tags` provide the user with a very useful tool to run
selected tasks of the role. To see what tags are available list them
using the command

.. include:: tags-list.rst

For example:

* Display the variables and their values usisng the tag
  ``poudriere_debug`` (enable debug ``poudriere_debug: true``) ::

   shell> ansible-playbook pb.yml -t poudriere_debug -e poudriere_debug=true

* See what packages will be installed (enable installation
  ``poudriere_install: true``) ::

   shell> ansible-playbook pb.yml -t poudriere_pkg -e poudriere_install=true --check

* Install packages and exit the play ::

   shell> ansible-playbook pb.yml -t poudriere_pkg -e poudriere_install=true

* See what packages lists will be created ::

   shell> ansible-playbook pb.yml -t poudriere_pkglists --check --diff

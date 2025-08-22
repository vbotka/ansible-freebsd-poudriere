.. _ug_vars:

Variables
---------

.. index:: single: defaults; Configuration/Variables
.. index:: single: package lists; Configuration/Variables

The default variables are stored in the directory ``defaults/main``.

.. seealso::

   * `Using Variables`_
   * `Ansible variable precedence - Where should I put a variable?`_
   * The examples of the customization `vars/main.yml.sample`_

.. _ug_vars_defaults:
.. include:: vars-defaults.rst

.. _ug_vars_packages:
.. include:: vars-packages.rst


.. _Using Variables: https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#using-variables
.. _Ansible variable precedence - Where should I put a variable?: https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable
.. _vars/main.yml.sample: https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/vars/main.yml.sample

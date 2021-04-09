.. _ug_debug:

Debug
-----

Enable debug output either in the configuration

.. code-block:: yaml
   :emphasize-lines: 1

   poudriere_debug: true

, or set the extra variable in the command

.. code-block:: console
   :emphasize-lines: 1

   shell> ansible-playbook pb.yml -e poudriere_debug=true

.. note::

   * The debug output of this role is optimized for the **yaml** callback plugin. Set this plugin
     for example in the environment ``shell> export ANSIBLE_STDOUT_CALLBACK=yaml``
   * See details about the yaml callback plugin ``shell> ansible-doc -t callback yaml``
   * See list of other callback plugins ``shell> ansible-doc -t callback -l``

.. seealso::

   * `Playbook Debugger <https://docs.ansible.com/ansible/latest/user_guide/playbooks_debugger.html>`_
   * `Debugging modules <https://docs.ansible.com/ansible/latest/dev_guide/debugging.html#debugging-modules>`_
   * `Python Debugging With Pdb <https://realpython.com/python-debugging-pdb/>`_

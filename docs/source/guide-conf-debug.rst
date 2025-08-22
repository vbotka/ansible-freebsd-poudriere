.. _ug_debug:

Debug
-----

Enable debug output either in the configuration

.. code-block:: yaml

   poudriere_debug: true

, or set the extra variable in the command. For example, display variables

.. code-block:: console

   shell> ansible-playbook pb.yml -t poudriere_debug -e poudriere_debug=true

.. hint::

   The debug output of this role is optimized for ``result_format=yaml``. See `result_format`_. Set
   it in the configuration

   .. code-block:: ini

      [defaults]
      callback_result_format = yaml

   , or in the environment

   .. code-block:: sh

      ANSIBLE_CALLBACK_RESULT_FORMAT=yaml

.. seealso::

   * `Playbook Debugger`_
   * `Debugging modules`_
   * `Python Debugging With Pdb`_


.. _result_format: https://docs.ansible.com/ansible/latest/collections/ansible/builtin/default_callback.html#parameter-result_format
.. _Playbook Debugger: https://docs.ansible.com/ansible/latest/user_guide/playbooks_debugger.html
.. _Debugging modules: https://docs.ansible.com/ansible/latest/dev_guide/debugging.html#debugging-modules
.. _Python Debugging With Pdb: https://realpython.com/python-debugging-pdb

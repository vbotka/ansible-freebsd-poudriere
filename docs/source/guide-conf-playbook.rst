.. _ug_playbook:

Playbook
--------

Create a simple playbook that calls this role (5) at a single host ``build.example.com`` (2)

.. code-block:: yaml
   :caption: pb.yml
   :emphasize-lines: 2,5
   :linenos:

   ---
   - hosts: build.example.com
     become: true
     roles:
       - vbotka.freebsd_poudriere

.. seealso::

   * `Understanding Privilege Escalation`_
   * `Working with playbooks`_

.. _Understanding Privilege Escalation: https://docs.ansible.com/ansible/latest/user_guide/become.html#understanding-privilege-escalation
.. _Working with playbooks: https://docs.ansible.com/ansible/latest/user_guide/playbooks.html

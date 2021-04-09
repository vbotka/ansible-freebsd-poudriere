.. _ug_playbook:

Playbook
--------

Create simple playbook that calls this role (6) at a single host build.example.com (3)

.. code-block:: yaml
   :emphasize-lines: 3,6
   :linenos:

   shell> cat pb.yml
   ---
   - hosts: build.example.com
     become: true
     roles:
       - vbotka.freebsd_poudriere

.. seealso::

   * `Understanding Privilege Escalation <https://docs.ansible.com/ansible/latest/user_guide/become.html#understanding-privilege-escalation>`_ (4)
   * `Working with playbooks <https://docs.ansible.com/ansible/latest/user_guide/playbooks.html>`_

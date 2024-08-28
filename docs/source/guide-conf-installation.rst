.. _ug_installation:

Installation
------------

The most convenient way to install an Ansible role is to use
:index:`Ansible Galaxy` CLI `ansible-galaxy`_. The utility comes with
the standard Ansible package and provides the user with a simple
interface to the Ansible Galaxy's services. For example, take a look
at the current status of the role ::

   shell> ansible-galaxy role info vbotka.freebsd_poudriere

and install it ::

   shell> ansible-galaxy role install vbotka.freebsd_poudriere

Install the collections if necessary ::

   shell> ansible-galaxy collection install community.crypto
   shell> ansible-galaxy collection install community.general
    
.. seealso::

   * To install specific versions from various sources see `Galaxy User Guide`_
   * Take a look at other roles. Run the command ::

        shell> ansible-galaxy search --author=vbotka

.. _`Galaxy User Guide`: https://docs.ansible.com/ansible/latest/galaxy/user_guide.html
.. _`ansible-galaxy`:  https://docs.ansible.com/ansible/latest/cli/ansible-galaxy.html

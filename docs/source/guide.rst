.. _ug:

############
User's guide
############
.. contents:: Table of Contents
   :depth: 4


.. _ug_introduction:

************
Introduction
************

* Ansible role: `freebsd_poudriere <https://galaxy.ansible.com/vbotka/freebsd_poudriere/>`_
* Supported systems: `FreeBSD <https://www.freebsd.org/releases/>`_
* Requirements: None

Poudriere is a BSD-licensed utility for creating and testing FreeBSD packages. To learn details see the references below

.. seealso::
   * FreeBSD Handbook `4.6. Building Packages with Poudriere <https://docs.freebsd.org/en_US.ISO8859-1/books/handbook/ports-poudriere.html>`_
   * FreeBSD Porter's Handbook `10.5. Poudriere <https://docs.freebsd.org/en/books/porters-handbook/index.html#testing-poudriere>`_
   * FreeBSD Wiki `Poudriere: Getting Started - Tutorial <https://wiki.freebsd.org/VladimirKrstulja/Guides/Poudriere>`_
   * DO Tutorials `How To Set Up a Poudriere Build System to Create Packages for your FreeBSD Servers <https://www.digitalocean.com/community/tutorials/how-to-set-up-a-poudriere-build-system-to-create-packages-for-your-freebsd-servers>`_


.. _ug_installation:

************
Installation
************

The most convenient way how to install an Ansible role is to use :index:`Ansible Galaxy` CLI
``ansible-galaxy``. The utility comes with the standard Ansible package and provides the user with a
simple interface to the Ansible Galaxy's services. For example, take a look at the current status of
the role

.. code-block:: console
   :emphasize-lines: 1

   shell> ansible-galaxy info vbotka.freebsd_poudriere

and install it

.. code-block:: console
   :emphasize-lines: 1

    shell> ansible-galaxy install vbotka.freebsd_poudriere

.. seealso::
   * To install specific versions from various sources see `Installing content <https://galaxy.ansible.com/docs/using/installing.html>`_
   * Take a look at other roles ``shell> ansible-galaxy search --author=vbotka``


.. _ug_playbook:

********
Playbook
********

Below is a simple playbook that calls this role (5) at a single host build.example.com (2)

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
   * See also `Understanding Privilege Escalation <https://docs.ansible.com/ansible/latest/user_guide/become.html#understanding-privilege-escalation>`_ (4)


.. _ug_debug:

*****
Debug
*****

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


.. _ug_tags:

****
Tags
****

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


.. _ug_vars:

*********
Variables
*********

.. seealso::
   * `Ansible variable precedence: Where should I put a variable?
     <https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable>`_

.. _ug_vars_defaults:
.. include:: vars-defaults.rst


.. _ug_examples:

*****
Tasks
*****

The description of the tasks is not complete. The `role <https://galaxy.ansible.com/vbotka/freebsd_poudriere/>`_ and the documentation is work in progress. Feel free to `share your feedback and report issues <https://github.com/vbotka/ansible-freebsd-poudriere/issues>`_.

`Contributions are welcome <https://github.com/firstcontributions/first-contributions>`_.

.. seealso::
   * Source code :ref:`as_main.yml`


.. _ug_task_packages:
.. include:: task-packages.rst
.. _ug_task_cert:
.. include:: task-cert.rst
.. _ug_task_conf:
.. include:: task-conf.rst
.. _ug_task_pkglist:
.. include:: task-pkglist.rst
.. _ug_task_make:
.. include:: task-make.rst


Examples
--------
.. toctree::
   :name: task1_toc

   task-task1-ex1
   task-task1-ex2

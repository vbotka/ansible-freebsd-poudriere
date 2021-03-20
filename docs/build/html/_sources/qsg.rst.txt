.. _qg:

Quick start guide
*****************

For the users who want to try the role quickly, this guide provides
an example of how to ...


* Install the role ``vbotka.freebsd_poudriere`` ::

    shell> ansible-galaxy install vbotka.freebsd_poudriere


* Create the playbook ``playbook.yml`` for single host srv.example.com (2)

.. code-block:: bash
   :emphasize-lines: 2
   :linenos:

   shell> cat playbook.yml
   - hosts: srv.example.com
     gather_facts: true
     connection: ssh
     remote_user: admin
     become: true
     become_user: root
     become_method: sudo
     roles:
       - vbotka.freebsd_poudriere


* Create ``host_vars`` with customized variables

.. code-block:: bash
   :emphasize-lines: 2
   :linenos:

   shell> ls -1 host_vars/srv.example.com/XY-*
   host_vars/srv.example.com/XY-*.yml


* To speedup the execution let's set some variables (2-4) to *false*

.. code-block:: bash
   :emphasize-lines: 2-4
   :linenos:

   shell> cat host_vars/srv.example.com/XY-common.yml
   XY_debug: false
   XY_backup_conf: false
   XY_flavors_enable: false


* Test syntax ::

    shell> ansible-playbook playbook.yml --syntax-check


* See what variables will be included ::

    shell> ansible-playbook playbook.yml -t XY_debug -e XY_debug=true


* Install packages ::

    shell> ansible-playbook playbook.yml -t XY_packages


* Dry-run, display differences and display variables ::

    shell> ansible-playbook playbook.yml -e XY_debug=true --check --diff


* Run the playbook ::

    shell> ansible-playbook playbook.yml


.. warning:: The host has not been secured by this playbook and should
             be used for testing only.

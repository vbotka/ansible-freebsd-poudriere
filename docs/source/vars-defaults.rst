Default variables
=================

[`defaults/main.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/defaults/main.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../defaults/main.yml
    :language: yaml
    :emphasize-lines: 2
    :linenos:


The common variables are sored in the file ``defaults/main.yml``. These variables can be customized
in the file ``vars/main.yml``. The file ``vars/main.yml`` will be preserved by the update of the
role.

.. warning::

   * Don't make any changes to the file *defaults/main.yml*. The changes will be overwritten by the
     update of the role. Customize the default values in the file *vars/main.yml*.

.. seealso::
   * The examples of the customization `vars/main.yml.sample <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/vars/main.yml.sample>`_

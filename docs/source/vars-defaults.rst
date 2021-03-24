Default variables
=================

[`defaults/main.yml <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/defaults/main.yml>`_]

.. highlight:: yaml
    :linenothreshold: 5
.. literalinclude:: ../../defaults/main.yml
    :language: yaml
    :emphasize-lines: 2
    :linenos:


The common variables are stored in the file ``defaults/main.yml`` (precedence 2.). In the scope of
the role, these variables can be customized in the file ``vars/main.yml`` (precedence 15.). The file
``vars/main.yml`` will be preserved by the update of the role.

.. warning::

   * *group_vars, host_vars, facts, play vars(_prompt, _files)* (precedence 3.-14.) can't override
     variables set in *vars/main.yml* (precedence 15.). As a result, *vars/main.yml* is not a
     suitable place to set values specific to the hosts or groups of the hosts. Instead, use it, for
     example, to set OS-specific values.

   * Don't make any changes to the file *defaults/main.yml*. An update of the role will overwrite
     it. Instead, customize the default values in the file *vars/main.yml*.

.. seealso::

   * The examples of the customization `vars/main.yml.sample <https://github.com/vbotka/ansible-freebsd-poudriere/blob/master/vars/main.yml.sample>`_

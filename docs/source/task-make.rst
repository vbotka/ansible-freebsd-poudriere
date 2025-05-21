Customize make
^^^^^^^^^^^^^^

.. index:: single: poudriere_make; Tasks/Customize make
.. index:: single: make; Tasks/Customize make

The customization of make.conf is enabled by default ::

   poudriere_make: true
   poudriere_make_file: "{{ poudriere_conf_dir }}/make.conf"

and the customization list is empty ::

   poudriere_make_conf: []

This would result in an empty file ``/usr/local/etc/poudriere.d/make.conf``. Optionally, set the
list of the options. For example, ::

   poudriere_make_conf:
     - "OPTIONS_UNSET+=\t\t\tDOCS NLS X11 EXAMPLES"
     - "OPTIONS_UNSET+=\t\t\tGSSAPI_BASE KRB_BASE KERBEROS"
     - "OPTIONS_SET+=\t\t\tGSSAPI_NONE KRB_NONE"
     - "DEFAULT_VERSIONS+=\t\temacs=nox"
     - "DEFAULT_VERSIONS+=\t\tphp=8.3"
     - "DEFAULT_VERSIONS+=\t\tssl=openssl"

Customize make.conf ::

   shell> ansible-playbook pb.yml -t poudriere_make

and take a look at the file

.. literalinclude:: example-make.txt
   :language: sh
   :linenos:
   :emphasize-lines: 1

.. seealso::
   * Source code :ref:`as_make.yml`
   * Template :ref:`as_template_make.conf.j2`
   * FreeBSD Porter's Handbook `5. Configuring the Makefile`_

.. _`5. Configuring the Makefile`: https://docs.freebsd.org/en/books/porters-handbook/makefiles/

Customize make
^^^^^^^^^^^^^^

By default, the customization of make.conf is enabled ::

  poudriere_make: true
  poudriere_make_file: "{{ poudriere_conf_dir }}/make.conf"

and the customization list is empty ::

  poudriere_make_conf: []

This would result in an empty file ``/usr/local/etc/poudriere.d/make.conf``. Optionally, set the
list of the options, e.g. ::

  poudriere_make_conf:
    - "OPTIONS_UNSET+=\t\t\tDOCS NLS X11 EXAMPLES"
    - "OPTIONS_UNSET+=\t\t\tGSSAPI_BASE KRB_BASE KERBEROS"
    - "OPTIONS_SET+=\t\t\tGSSAPI_NONE KRB_NONE"
    - "DEFAULT_VERSIONS+=\t\temacs=nox"
    - "DEFAULT_VERSIONS+=\t\tphp=7.2"
    - "DEFAULT_VERSIONS+=\t\tssl=openssl"

Customize make.conf ::

  shell> ansible-playbook pb.yml -t poudriere_make

and review the file ::

  [root@build /usr/home/admin]# cat /usr/local/etc/poudriere.d/make.conf
  # Ansible managed
  OPTIONS_UNSET+=		DOCS NLS X11 EXAMPLES
  OPTIONS_UNSET+=		GSSAPI_BASE KRB_BASE KERBEROS
  OPTIONS_SET+=			GSSAPI_NONE KRB_NONE
  DEFAULT_VERSIONS+=		emacs=nox
  DEFAULT_VERSIONS+=		php=7.2
  DEFAULT_VERSIONS+=		ssl=openssl


.. seealso::
   * Source code :ref:`as_make.yml`
   * Template :ref:`as_template_make.conf.j2`
   * FreeBSD Porter's Handbook  `10.5.10. Providing a Custom make.conf File <https://docs.freebsd.org/en/books/porters-handbook/#testing-poudriere>`_

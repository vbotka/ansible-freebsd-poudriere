.. code-block:: yaml
   :caption: shell> ansible-playbook pb.yml -t poudriere_make
   :linenos:
   :force:

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Make: Configure /usr/local/etc/poudriere.d/make.conf] *****************
   changed: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=2    changed=1    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0

.. code-block:: make
   :caption: /usr/local/etc/poudriere.d/make.conf

   # Ansible managed
   OPTIONS_UNSET+=	DOCS NLS X11 EXAMPLES
   OPTIONS_UNSET+=	GSSAPI_BASE KRB_BASE KERBEROS
   OPTIONS_SET+=	GSSAPI_NONE KRB_NONE
   DEFAULT_VERSIONS+=	emacs=nox
   DEFAULT_VERSIONS+=	php=8.3
   DEFAULT_VERSIONS+=	ssl=openssl

.. code-block:: sh
   :emphasize-lines: 1,11,20
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_packages -e poudriere_install=true

   PLAY [build.example.com] ********************************************************************************

   TASK [Gathering Facts] **********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Pkg: Install poudriere packages] ***************************************
   changed: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Pkg: Install poudriere ports] ******************************************
   skipping: [build.example.com] => (item=ports-mgmt/poudriere) 
   skipping: [build.example.com] => (item=ports-mgmt/portmaster) 
   skipping: [build.example.com] => (item=devel/ccache) 
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Pkg: Install packages to create certificate] ***************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Pkg: Install ports to create certificate] ******************************
   skipping: [build.example.com] => (item=security/py-openssl) 
   skipping: [build.example.com] => (item=security/py-acme-tiny) 
   skipping: [build.example.com]

   PLAY RECAP **********************************************************************************************
   build.example.com: ok=3    changed=1    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0

.. code-block:: sh
   :emphasize-lines: 1,11,17,20,23
   :linenos:

   shell> ansible-playbook pb.yml -t poudriere_cert -e poudriere_cert=true

   PLAY [build.example.com] *******************************************************************************

   TASK [Gathering Facts] *********************************************************************************
   ok: [build.example.com]

   TASK [vbotka.freebsd_poudriere : Poudriere Debug] ******************************************************
   skipping: [build.example.com]

   TASK [vbotka.freebsd_poudriere : cert: Create directories] *********************************************
   ok: [build.example.com] => (item=/usr/local/etc/ssl)
   ok: [build.example.com] => (item=/usr/local/etc/ssl/crt)
   ok: [build.example.com] => (item=/usr/local/etc/ssl/csr)
   ok: [build.example.com] => (item=/usr/local/etc/ssl/private)

   TASK [vbotka.freebsd_poudriere : cert: Generate an OpenSSL private key (default 4096 bits, RSA)] *******
   changed: [build.example.com]

   TASK [vbotka.freebsd_poudriere : cert: Generate an OpenSSL Certificate Signing Request] ****************
   changed: [build.example.com]

   TASK [vbotka.freebsd_poudriere : cert: Generate a Self Signed OpenSSL certificate] *********************
   changed: [build.example.com]

   PLAY RECAP *********************************************************************************************
   build.example.com: ok=5    changed=3    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0


.. code-block:: sh
   :emphasize-lines: 1,6,9,11
   :linenos:

   shell> tree /usr/local/etc/ssl/
   /usr/local/etc/ssl/
   |-- cert.pem
   |-- cert.pem.sample -> ../../share/certs/ca-root-nss.crt
   |-- certs
   |   `-- build.example.com.crt
   |-- crt
   |-- csr
   |   `-- build.example.com.csr
   `-- private
       `-- build.example.com.key

.. code-block:: bash
   :emphasize-lines: 1,3
   :linenos:

   shell> cat pb.yml
   ---
   - hosts: build.example.com
     become: true
     roles:
       - vbotka.freebsd_poudriere

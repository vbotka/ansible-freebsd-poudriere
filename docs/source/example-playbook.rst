.. code-block:: yaml
   :caption: pb.yml 
   :emphasize-lines: 2
   :linenos:

   ---
   - hosts: build.example.com
     gather_facts: true
     become: true
     roles:
       - vbotka.freebsd_poudriere

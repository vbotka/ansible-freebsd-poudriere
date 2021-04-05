.. _ug_example_ports_create:

Create ports
------------

.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   [root@build /usr/home/admin]# poudriere ports -c -p local
   [00:00:00] Creating local fs at /zroot/poudriere/ports/local... done
   [00:00:00] Checking out the ports tree... done


Optionaly update ports tree if it has already been created

.. code-block:: sh
   :emphasize-lines: 1
   :linenos:

   [root@build /usr/home/admin]# poudriere ports -u -p local
   [00:00:00] Creating local fs at /zroot/poudriere/ports/local... done
   [00:00:00] Checking out the ports tree... done

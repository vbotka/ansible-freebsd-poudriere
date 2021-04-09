.. _ug_client:

Configure clients
-----------------

Log to the client and configure the repository ::

  root@generic:/home/admin # uname -a
  FreeBSD generic 12.2-STABLE FreeBSD 12.2-STABLE r369071 GENERIC  arm

  root@generic:/home/admin # cat /usr/local/etc/pkg/repos/poudriere.conf
  poudriere: {
      url: "http://build.example.com/packages/12arm7-local-devel",
      mirror_type: "http",
      enabled: yes,
      priority: 100,
      signature_type: "pubkey",
      pubkey: "/usr/local/etc/ssl/certs/build.example.com-sk.crt"
  }

Disable the official repositories ::

  root@generic:/home/admin # cat /usr/local/etc/pkg/repos/freebsd.conf
  FreeBSD: {
      enabled: no
  }

Update your pkg database ::

  root@generic:/home/admin # pkg update
  Updating poudriere repository catalogue...
  Fetching meta.conf: 100%    163 B   0.2kB/s    00:01
  Fetching packagesite.txz: 100%   42 KiB  42.8kB/s    00:01
  Processing entries: 100%
  poudriere repository update completed. 145 packages processed.
  All repositories are up to date.

Display details ::

  root@generic:/home/admin # pkg -vv
  ...
  Repositories:
  poudriere: {
    url             : "http://build.example.com/packages/12arm7-local-devel",
    enabled         : yes,
    priority        : 100,
    mirror_type     : "HTTP",
    signature_type  : "PUBKEY",
    pubkey          : "/usr/local/etc/ssl/certs/build.example.com-sk.crt"
  }

.. note::

   It seems, it's not possible to force *pkg* accept self-signed https certificate. Settting
   ``url: "https:// build ...`` without verified certificate results in the error
   ``SSL routines:tls_process_server_certificate:certificate verify failed``
   ``pkg: https://build.example.com/ ... /packagesite.txz: Authentication error``
   See `DO comment <https://www.digitalocean.com/community/tutorials/how-to-set-up-a-poudriere-build-system-to-create-packages-for-your-freebsd-servers?comment=97460>`_.


Manage packages ::

  root@generic:/home/admin # pkg info | grep pkg
  pkg-1.15.10                    Package manager

  root@generic:/home/admin # pkg upgrade pkg
  Updating poudriere repository catalogue...
  poudriere repository is up to date.
  All repositories are up to date.
  New version of pkg detected; it needs to be installed first.
  The following 1 package(s) will be affected (of 0 checked):

  Installed packages to be UPGRADED:
  pkg: 1.15.10 -> 1.16.3

  Number of packages to be upgraded: 1

  The process will require 2 MiB more space.
  7 MiB to be downloaded.

  Proceed with this action? [y/N]: y
  [1/1] Fetching pkg-1.16.3.txz: 100%    7 MiB   7.0MB/s    00:01
  Checking integrity... done (0 conflicting)
  [1/1] Upgrading pkg from 1.15.10 to 1.16.3...
  [1/1] Extracting pkg-1.16.3: 100%
  Updating poudriere repository catalogue...
  poudriere repository is up to date.
  All repositories are up to date.
  Checking integrity... done (0 conflicting)
  Your packages are up to date.


.. seealso::

  * FreeBSD Handbook `4.6.2. Configuring pkg Clients to Use a Poudriere Repository <https://docs.freebsd.org/en_US.ISO8859-1/books/handbook/ports-poudriere.html>`_
  * man `pkg(8) <https://www.freebsd.org/cgi/man.cgi?query=pkg&sektion=&n=1>`_
  * man `pkg.conf(5) <https://www.freebsd.org/cgi/man.cgi?query=pkg.conf&sektion=5&n=1>`_

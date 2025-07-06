==========================================
vbotka.freebsd_poudriere 2.7 Release Notes
==========================================

.. contents:: Topics


2.7.4
=====

Release Summary
---------------


2.7.3
=====

Release Summary
---------------
Maintenance update.

Major Changes
-------------

Minor Changes
-------------
* Supported FreeBSD 13.4, 13.5, 14.2, 14.3
* Updated docs. Updated annotation templates.


2.7.2
=====

Release Summary
---------------
Updated docs.


2.7.1
=====

Release Summary
---------------
Maintenance update.

Major Changes
-------------

Minor Changes
-------------
* Updated tasks formatting.


2.7.0
=====

Release Summary
---------------
Ansible 2.18 update.

Major Changes
-------------
* Supported 13.4, 13.5, and 14.2
* Added var freebsd_iocage_env (default={CRYPTOGRAPHY_OPENSSL_NO_LEGACY: '1'})
* Added var poudriere_packages_use_globs (default=false)
* Added .gitignore

Minor Changes
-------------
* Split defaults/main.yml into files defaults/main/\*.yml
* Added tasks/sanity.yml (default poudriere_sanity=false)
* Updated documentation. Updated annotation templates
* Variable freebsd_use_packages is not mandatory (default=omit)

Bugfixes
--------

Breaking Changes / Porting Guide
--------------------------------

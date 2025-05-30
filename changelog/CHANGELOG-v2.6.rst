==========================================
vbotka.freebsd_poudriere 2.6 Release Notes
==========================================

.. contents:: Topics


2.6.3
=====

Release Summary
---------------
Update docs.

Major Changes
-------------

Minor Changes
-------------
* Update docs.


2.6.2
=====

Release Summary
---------------
Update docs.

Major Changes
-------------

Minor Changes
-------------
- Update docs.


2.6.1
=====

Release Summary
---------------
Maintenance including docs update.

Major Changes
-------------
* Update docs
* Add Pkglist: Assert all items in _pkglist_enable are available in _pkg_dict

Minor Changes
-------------
- Update python 3.11 in .travis.yml
- Update tests/test.yml playbook


2.6.0
=====

Release Summary
---------------
Ansible 2.17 maintenance and features including docs update.

Major Changes
-------------
* Supported 13.3, 14.0, and 14.1
* Update docs

Minor Changes
-------------
* Update README, lint conf, meta, and travis conf
* Fix lint.
* Update debug.yml
* Add variable poudriere_role_version
* Update pkglist.yml
* Add variable poudriere_pkglist_all default=false. Create files "All"
  if enabled.

Bugfixes
--------

Breaking Changes / Porting Guide
--------------------------------
* The default directory for packages lists is
  "/usr/local/etc/poudriere.d/pkglist/{{ pkg_arch }}"
* The variable pkglist_enable_{{ pkg_arch }}" is a plain list of
  anabled lists.
* Optional attribute "enable" in "pkg_dict_{{ pkg_arch }}" is
  ignored. All lists will be created in the directory "pkglist/{{
  pkg_arch }}". Optionally, use "pkglist_enable_{{ pkg_arch }}" to
  link enabled lists in the directory "pkglist/{{ pkg_arch }}.enabled*

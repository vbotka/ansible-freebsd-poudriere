freebsd-poudriere
=================

[![Build Status](https://travis-ci.org/vbotka/ansible-freebsd-poudriere.svg?branch=master)](https://travis-ci.org/vbotka/ansible-freebsd-poudriere)

[Ansible role.](https://galaxy.ansible.com/vbotka/freebsd-poudriere/) Install and configure Poudriere Build System in FreeBSD.


Requirements
------------

No requiremenst.


Variables
---------

TBD (Check the defaults).


Workflow
--------

1) Change shell to /bin/sh if necessary.

```
ansible host -e 'ansible_shell_type=csh ansible_shell_executable=/bin/csh' -a 'sudo pw usermod admin -s /bin/sh'
```

2) Install role.

```
ansible-galaxy install vbotka.freebsd-poudriere
```

3) Fit variables.

```
~/.ansible/roles/vbotka.freebsd-poudriere/vars/main.yml
```

4) Create and run the playbook.

```
> cat ~/.ansible/playbooks/freebsd-poudriere.yml
---
- hosts: host
  become: yes
  become_method: sudo
  roles:
    - role: vbotka.freebsd-poudriere
    
> ansible-playbook ~/.ansible/playbooks/freebsd-poudriere.yml
```

Build packages
--------------

ssh to the host, create jail with the required FreeBSD tree and a ports tree, configure and build the packages.
```
# poudriere jail -c -j 11amd64 -v 11.1-RELEASE
# poudriere ports -c -p local
# poudriere options -j 11amd64 -p local -f 11amd64-pkglist
# poudriere builk -j 11amd64 -p local -f 11amd64-pkglist
```


References
----------

- [Building Packages with Poudriere](http://www.freebsd.cz/doc/handbook/ports-poudriere.html)
- [Poudriere wiki](https://github.com/freebsd/poudriere/wiki)
- [How To Set Up a Poudriere Build System](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-poudriere-build-system-to-create-packages-for-your-freebsd-servers)

License
-------

[![license](https://img.shields.io/badge/license-BSD-red.svg)](https://www.freebsd.org/doc/en/articles/bsdl-gpl/article.html)


Author Information
------------------

[Vladimir Botka](https://botka.link)

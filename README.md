freebsd-poudriere
=================

[![Build Status](https://travis-ci.org/vbotka/ansible-freebsd-poudriere.svg?branch=master)](https://travis-ci.org/vbotka/ansible-freebsd-poudriere)

[Ansible role.](https://galaxy.ansible.com/vbotka/freebsd-poudriere/) Install and configure Poudriere Build System in FreeBSD.


Requirements
------------

No requiremenst. Tested with FreeBSD 11.2


Variables
---------

TBD (Check the defaults).


Workflow
--------

1) Change shell to /bin/sh if necessary.

```
# ansible host -e 'ansible_shell_type=csh ansible_shell_executable=/bin/csh' -a 'sudo pw usermod admin -s /bin/sh'
```

2) Install role.

```
# ansible-galaxy install vbotka.freebsd-poudriere
```

3) Fit variables.

```
# editor vbotka.freebsd-poudriere/vars/main.yml
```

4) Create and run the playbook.

```
# cat freebsd-poudriere.yml

- hosts: build.example.com
  roles:
    - vbotka.freebsd-poudriere
```

```
# ansible-playbook freebsd-poudriere.yml
```


Build packages
--------------

1) ssh to the host.

2) Optionally copy existing PORT_DBDIR to the directory
*/usr/local/etc/poudriere.d/options* and review the options.

3) Create the jail *11amd64* with the required FreeBSD tree
*11.2-RELEASE*

```
# poudriere jail -c -j 11amd64 -v 11.2-RELEASE
```

4) Create ports tree *local*

```
# poudriere ports -c -p local
```


5) Configure the options for the packages *pkglist*. This will
supperseed the options from step 2.

```
# poudriere options -j 11amd64 -p local -z setname -f pkglist
```

6) Build the set of packages *setname* listed in *pkglist*.

```
# poudriere bulk -j 11amd64 -p local -z setname -f pkglist
```

3) Provide the clients with the certificate */usr/local/etc/ssl/crt/poudriere.crt*

4) Install a web server and publish the packages
*/usr/local/poudriere/data/packages/11amd64-local-setname*


References
----------

- [FreBSD handbook: Building Packages with Poudriere](http://www.freebsd.org/doc/handbook/ports-poudriere.html)
- [FreBSD porter's handbook: Poudriere](http://www.freebsd.org/doc/en/books/porters-handbook/testing-poudriere.html)
- [Poudriere wiki](https://github.com/freebsd/poudriere/wiki)
- [DigitalOcean: How To Set Up a Poudriere Build System](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-poudriere-build-system-to-create-packages-for-your-freebsd-servers)
- [Building packages with poudriere](https://stevendouglas.me/?p=71)

License
-------

[![license](https://img.shields.io/badge/license-BSD-red.svg)](https://www.freebsd.org/doc/en/articles/bsdl-gpl/article.html)


Author Information
------------------

[Vladimir Botka](https://botka.link)

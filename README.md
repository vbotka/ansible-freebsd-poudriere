# freebsd_poudriere

[![quality](https://img.shields.io/ansible/quality/27910)](https://galaxy.ansible.com/vbotka/freebsd_poudriere)[![Build Status](https://travis-ci.org/vbotka/ansible-freebsd-poudriere.svg?branch=master)](https://travis-ci.org/vbotka/ansible-freebsd-poudriere)

[Ansible role.](https://galaxy.ansible.com/vbotka/freebsd_poudriere/) FreeBSD. Install and configure Poudriere Build System.

Feel free to [share your feedback and report issues](https://github.com/vbotka/ansible-freebsd-poudriere/issues).

[Contributions are welcome](https://github.com/firstcontributions/first-contributions).


## Requirements

None.


## Role Variables

Review the defaults and examples in vars.


## Workflow

1) Change shell to /bin/sh if necessary

```
shell> ansible host -e 'ansible_shell_type=csh ansible_shell_executable=/bin/csh' -a 'sudo pw usermod admin -s /bin/sh'
```

2) Install role

```
shell> ansible-galaxy install vbotka.freebsd_poudriere
```

3) Fit variables

```
shell> editor vbotka.freebsd_poudriere/vars/main.yml
```

4) Create and run the playbook

```
shell> cat freebsd-poudriere.yml

- hosts: build.example.com
  roles:
    - vbotka.freebsd_poudriere
```

```
shell> ansible-playbook freebsd-poudriere.yml
```


## Build packages

1) ssh to the host.

2) Optionally copy existing PORT_DBDIR to the directory */usr/local/etc/poudriere.d/options* and review the options.

3) Create the jail *11amd64* with the required FreeBSD tree *11.2-RELEASE*

```
shell> poudriere jail -c -j 11amd64 -v 11.2-RELEASE
```

4) Create ports tree *local*

```
shell> poudriere ports -c -p local
```

5) Configure the options for the packages *pkglist*. This will supersede the options from step 2.

```
shell> poudriere options -j 11amd64 -p local -z setname -f pkglist
```

6) Build the set of packages *setname* listed in *pkglist*.

```
shell> poudriere bulk -j 11amd64 -p local -z setname -f pkglist
```

7) Provide the clients with the certificate */usr/local/etc/ssl/crt/poudriere.crt*

8) Install a web server and publish the packages
*/usr/local/poudriere/data/packages/11amd64-local-setname*


## Clients

1) Configure the repositories with [Ansible role freebsd_packages](https://galaxy.ansible.com/vbotka/freebsd_packages/) and install the packages (with Ansible module pkgng).

2) Alternatively set *freebsd_use_packages:yes* and install the packages with [Ansible role freebsd_ports](https://galaxy.ansible.com/vbotka/freebsd_ports/) (with Ansible module portinstall).


## References

- [FreBSD handbook: Building Packages with Poudriere](http://www.freebsd.org/doc/handbook/ports-poudriere.html)
- [FreBSD porter's handbook: Poudriere](http://www.freebsd.org/doc/en/books/porters-handbook/testing-poudriere.html)
- [Poudriere wiki](https://github.com/freebsd/poudriere/wiki)
- [DigitalOcean: How To Set Up a Poudriere Build System](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-poudriere-build-system-to-create-packages-for-your-freebsd-servers)
- [Building packages with poudriere](https://stevendouglas.me/?p=71)


## License

[![license](https://img.shields.io/badge/license-BSD-red.svg)](https://www.freebsd.org/doc/en/articles/bsdl-gpl/article.html)


## Author Information

[Vladimir Botka](https://botka.link)

# freebsd_poudriere

[![quality](https://img.shields.io/ansible/quality/27910)](https://galaxy.ansible.com/vbotka/freebsd_poudriere)[![Build Status](https://travis-ci.org/vbotka/ansible-freebsd-poudriere.svg?branch=master)](https://travis-ci.org/vbotka/ansible-freebsd-poudriere)[![Documentation Status](https://readthedocs.org/projects/docs/badge/?version=latest)](https://ansible-freebsd-popoudriere.readthedocs.io/en/latest/)

[Ansible role.](https://galaxy.ansible.com/vbotka/freebsd_poudriere/) FreeBSD. Install and configure Poudriere Build System.

[Documentation at readthedocs.io]( https://ansible-freebsd-poudriere.readthedocs.io)

Feel free to [share your feedback and report issues](https://github.com/vbotka/ansible-freebsd-poudriere/issues). [Contributions are welcome](https://github.com/firstcontributions/first-contributions).


## Supported platforms

This role has been developed and tested with [FreeBSD Supported Releases](https://www.freebsd.org/releases/).


## Requirements

None.


## Variables

Review the defaults and examples in vars.


## Workflow

* Change the login shell for the remote_user at the remote host build.example.com to /bin/sh if necessary

```
shell> ansible build.example.com -e 'ansible_shell_type=csh ansible_shell_executable=/bin/csh' -a 'sudo pw usermod admin -s /bin/sh'
```

* Install role

```
shell> ansible-galaxy install vbotka.freebsd_poudriere
```

* Fit variables

```
shell> editor vbotka.freebsd_poudriere/vars/main.yml
```

* Create and run the playbook

```
shell> cat freebsd-poudriere.yml

- hosts: build.example.com
  roles:
    - vbotka.freebsd_poudriere
```

```
shell> ansible-playbook freebsd-poudriere.yml
```


## Example: Build packages for amd64 in 11.2-RELEASE

* ssh to the host build.example.com

* Optionally copy existing PORT_DBDIR to the directory */usr/local/etc/poudriere.d/options* and
  review the options.

* Create the jail *11amd64* with the required FreeBSD tree *11.2-RELEASE*

```
shell> poudriere jail -c -j 11amd64 -v 11.2-RELEASE
```

* Create ports tree *local*

```
shell> poudriere ports -c -p local
```

* Review the lists of the packages. See tasks/pkglist.yml
  (default: {{ poudriere_pkglist_dir }}_{{ pkg_arch }})

```
shell: ls -la /usr/local/etc/poudriere.d/pkglist_amd64
```

  For example

```
shell> cat /usr/local/etc/poudriere.d/pkglist_amd64/minimal
shells/bash
devel/git
archivers/gtar
ports-mgmt/pkg
ports-mgmt/portmaster
ports-mgmt/portupgrade
net/rsync
ftp/wget
```

* Optionally configure the options for the packages *pkglist*. This will supersede the options from
  step 2. See Handbook 10.5.9. Using Sets

```
shell> poudriere options -j 11amd64 -p local -z setname -f pkglist
```

* Build the set of packages *setname* listed in the file /usr/local/etc/poudriere.d/pkglist_amd64/minimal

```
shell> poudriere bulk -j 11amd64 -p local -z setname -f /usr/local/etc/poudriere.d/pkglist_amd64/minimal
```

* ,or build the set of packages *setname* listed in in the files /usr/local/etc/poudriere.d/pkglist_amd64/*

```
shell> for i in /usr/local/etc/poudriere.d/pkglist_amd64/*; do poudriere bulk -j 11amd64 -p local -z setname -f $i; done
```

* Provide the clients with the certificate. (default poudriere_cert_path)

```
/usr/local/etc/ssl/crt/poudriere.crt
```

* Install a web server and publish the packages

```
/usr/local/poudriere/data/packages/11amd64-local-setname
```


## Clients

* Use [Ansible role freebsd_packages](https://galaxy.ansible.com/vbotka/freebsd_packages/) to
  configure the repositories and to install the packages using Ansible module pkgng.

* Alternatively set *freebsd_use_packages=true* and use [Ansible role freebsd_ports](https://galaxy.ansible.com/vbotka/freebsd_ports/) to install the packages using
  Ansible module portinstall.


## References

- [FreBSD Handbook: Building Packages with Poudriere](http://www.freebsd.org/doc/handbook/ports-poudriere.html)
- [FreBSD Porter's Handbook: Poudriere](http://www.freebsd.org/doc/en/books/porters-handbook/testing-poudriere.html)
- [Poudriere Wiki](https://github.com/freebsd/poudriere/wiki)
- [DigitalOcean: How To Set Up a Poudriere Build System](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-poudriere-build-system-to-create-packages-for-your-freebsd-servers)
- [Building packages with Poudriere](https://stevendouglas.me/?p=71)


## License

[![license](https://img.shields.io/badge/license-BSD-red.svg)](https://www.freebsd.org/doc/en/articles/bsdl-gpl/article.html)


## Author Information

[Vladimir Botka](https://botka.link)

# freebsd_poudriere

[![quality](https://img.shields.io/ansible/quality/27910)](https://galaxy.ansible.com/vbotka/freebsd_poudriere)
[![Build Status](https://travis-ci.org/vbotka/ansible-freebsd-poudriere.svg?branch=master)](https://travis-ci.org/vbotka/ansible-freebsd-poudriere)
[![Documentation Status](https://readthedocs.org/projects/docs/badge/?version=latest)](https://ansible-freebsd-poudriere.readthedocs.io/en/latest/)
[![GitHub tag](https://img.shields.io/github/v/tag/vbotka/ansible-freebsd-poudriere)](https://github.com/vbotka/ansible-freebsd-poudriere/tags)

This role is included in the collection [vbotka.freebsd](https://galaxy.ansible.com/ui/repo/published/vbotka/freebsd/) as [vbotka.freebsd.poudriere](https://galaxy.ansible.com/ui/repo/published/vbotka/freebsd/content/role/poudriere)

[Ansible role.](https://galaxy.ansible.com/vbotka/freebsd_poudriere/) FreeBSD. Install and configure Poudriere Build System.

[Documentation at readthedocs.io]( https://ansible-freebsd-poudriere.readthedocs.io)

Feel free to [share your feedback and report issues](https://github.com/vbotka/ansible-freebsd-poudriere/issues).

[Contributions are welcome](https://github.com/firstcontributions/first-contributions).


## Supported platforms

This role is developed and tested with [FreeBSD Supported Releases](https://www.freebsd.org/releases/).


## Requirements

### Collections

- community.crypto
- community.general


## Variables

Look at the *defaults* and examples in *vars*.


## Workflow

* Change the login shell for the remote_user at the remote host build.example.com to /bin/sh if necessary

```bash
shell> ansible build.example.com -e 'ansible_shell_type=csh ansible_shell_executable=/bin/csh' -a 'sudo pw usermod admin -s /bin/sh'
```

* Install the role and the collections

```bash
shell> ansible-galaxy role install vbotka.freebsd_poudriere
```

Install the collections if necessary

```bash
shell> ansible-galaxy collection install community.crypto
shell> ansible-galaxy collection install community.general
```

* Fit variables to your needs.

* Create the playbook freebsd-poudriere.yml

```yaml
- hosts: build.example.com
  roles:
    - vbotka.freebsd_poudriere
```

* Check syntax

```bash
shell> ansible-playbook freebsd-poudriere.yml --syntax-check
```

* Display variables

```bash
shell> ansible-playbook freebsd-poudriere.yml -t poudriere_debug -e poudriere_debug=true
```

* Install packages

```bash
shell> ansible-playbook freebsd-poudriere.yml -t poudriere_pkg -e poudriere_install=true
```

* Run the playbook and configure poudriere

```bash
shell> ansible-playbook freebsd-poudriere.yml
```


## Example: Build 14.1-RELEASE packages for amd64

* ssh to the host build.example.com

* Optionally copy existing PORT_DBDIR to the directory */usr/local/etc/poudriere.d/options* and
  review the options.

* Create the jail *14Ramd64* from the FreeBSD *14.1-RELEASE* tree

```bash
shell> poudriere jail -c -j 141Ramd64 -v 14.1-RELEASE -a amd64
```

* Create ports

```bash
shell> poudriere ports -c -m git+https -B main
```

* Take a look at the packages lists. See tasks/pkglist.yml (default: {{ poudriere_pkglist_dir }}/{{ pkg_arch }})

```bash
shell: ls -la /usr/local/etc/poudriere.d/pkglist/amd64
```

For example,

```bash
shell> cat /usr/local/etc/poudriere.d/pkglist/amd64/minimal
shells/bash
devel/git
archivers/gtar
ports-mgmt/pkg
ports-mgmt/portmaster
ports-mgmt/portupgrade
net/rsync
ftp/wget
```

* Optionally, configure the options for the packages *pkglist*. This will supersede the options from
  step 2. See the Handbook: Building Packages with poudriere. Using Sets.

```bash
shell> poudriere options -j 141Ramd64 -z <setname> -f pkglist
```

* Build the set of packages *setname* listed in the file /usr/local/etc/poudriere.d/pkglist/amd64/minimal

```bash
shell> poudriere bulk -j 141Ramd64 -z devel -f /usr/local/etc/poudriere.d/pkglist/amd64/minimal
```

* Provide the clients with the certificate. (default poudriere_cert_path)

```bash
/usr/local/etc/ssl/crt/poudriere.crt
```

* Install a web server and publish the packages

```bash
/usr/local/poudriere/data/packages/14amd64-local-setname
```


## Clients

* Use [Ansible role freebsd_packages](https://galaxy.ansible.com/vbotka/freebsd_packages/) to
  configure the repositories and to install the packages using Ansible module *community.general.pkgng*.

* Alternatively set *freebsd_use_packages=true* and use [Ansible role freebsd_ports](https://galaxy.ansible.com/vbotka/freebsd_ports/) to install the packages using
  Ansible module *community.general.portinstall*.


## Ansible lint

Use the configuration file *.ansible-lint.local* when running *ansible-lint*. Some rules might be
disabled and some warnings might be ignored. See the notes in the configuration file.

```bash
shell> ansible-lint -c .ansible-lint.local
```


## References

- [FreBSD Handbook: Building Packages with Poudriere](https://docs.freebsd.org/en/books/handbook/ports/#ports-poudriere)
- [FreBSD Porter's Handbook: Poudriere](http://www.freebsd.org/doc/en/books/porters-handbook/testing-poudriere.html)
- [Poudriere Wiki](https://github.com/freebsd/poudriere/wiki)
- [DigitalOcean: How To Set Up a Poudriere Build System](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-poudriere-build-system-to-create-packages-for-your-freebsd-servers)
- [Building packages with Poudriere](https://stevendouglas.me/?p=71)


## License

[![license](https://img.shields.io/badge/license-BSD-red.svg)](https://www.freebsd.org/doc/en/articles/bsdl-gpl/article.html)


## Author Information

[Vladimir Botka](https://botka.info)

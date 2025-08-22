.. code-block:: console
   :caption: shell> poudriere jail -c -j 141Ramd64 -v 14.1-RELEASE -a amd64

   [00:00:00] Creating 141Ramd64 fs at /usr/local/poudriere/jails/141Ramd64... done
   [00:00:00] Using pre-distributed MANIFEST for FreeBSD 14.1-RELEASE amd64
   [00:00:00] Fetching base for FreeBSD 14.1-RELEASE amd64
   base.txz                                               198 MB   10 MBps    18s
   [00:00:21] Extracting base... done
   [00:00:47] Fetching src for FreeBSD 14.1-RELEASE amd64
   src.txz                                                205 MB   10 MBps    20s
   [00:01:09] Extracting src... done
   [00:01:53] Fetching lib32 for FreeBSD 14.1-RELEASE amd64
   lib32.txz                                               60 MB    9 MBps    06s
   [00:02:00] Extracting lib32... done
   [00:02:06] Cleaning up... done
   [00:02:06] Recording filesystem state for clean... done
   [00:02:06] Upgrading using http
   Looking up update.FreeBSD.org mirrors... 3 mirrors found.
   Fetching public key from update2.freebsd.org... done.
   Fetching metadata signature for 14.1-RELEASE from update2.freebsd.org... done.
   Fetching metadata index... done.
   Fetching 2 metadata files... done.
   ...
   [00:04:58] Recording filesystem state for clean... done
   [00:04:58] Jail 141Ramd64 14.1-RELEASE-p3 amd64 is ready to be used

.. code-block:: console
   :caption: shell> poudriere ports -c -m git+https -B main

   [00:00:00] Creating default fs at /usr/local/poudriere/ports/default... done
   [00:00:00] Cloning the ports tree... done

.. code-block:: sh
   :caption: shell> poudriere bulk -j 141Ramd64 -z devel -f /usr/local/etc/poudriere.d/pkglist/amd64/minimal

   [00:00:00] Creating the reference jail... done
   [00:00:05] Mounting system devices for 141Ramd64-default-devel
   [00:00:06] Converting package repository to new format
   [00:00:06] Stashing existing package repository
   [00:00:06] Mounting ports from: /usr/local/poudriere/ports/default
   [00:00:06] Mounting packages from: /usr/local/poudriere/data/packages/141Ramd64-default-devel
   [00:00:06] Mounting distfiles from: /usr/ports/distfiles
   [00:00:06] Appending to make.conf: /usr/local/etc/poudriere.d/make.conf /etc/resolv.conf -> /usr/local/poudriere/data/.m/141Ramd64-default-devel/ref/etc/resolv.conf
   [00:00:06] Starting jail 141Ramd64-default-devel
   [00:00:06] Will build as nobody:nobody (65534:65534)
   [00:00:07] Logs: /usr/local/poudriere/data/logs/bulk/141Ramd64-default-devel/2024-08-08_22h56m31s
   [00:00:07] WWW: http://build.example.com/build.html?mastername=141Ramd64-default-devel&build=2024-08-08_22h56m31s
   [00:00:07] Loading MOVED for /usr/local/poudriere/data/.m/141Ramd64-default-devel/ref/usr/ports
   [00:00:08] Ports supports: FLAVORS SUBPACKAGES SELECTED_OPTIONS
   [00:00:08] Inspecting ports tree for modifications to git checkout... no
   [00:00:12] Ports top-level git hash: 88c12b53a 
   [00:00:12] Gathering ports metadata
   [00:00:13] Calculating ports order and dependencies
   [00:00:14] Trimming IGNORED and blacklisted ports
   [00:00:14] pkg bootstrap missing: unable to inspect existing packages, cleaning all packages... done
   [00:00:14] Sanity checking the repository
   [00:00:14] Deleting stale symlinks... done
   [00:00:14] Deleting empty directories... done
   [00:00:14] Unqueueing existing packages
   [00:00:14] Unqueueing orphaned build dependencies
   [00:00:15] Sanity checking build queue
   [00:00:15] Processing PRIORITY_BOOST
   [00:00:15] Balancing pool
   [141Ramd64-default-devel] [2024-08-08_22h56m31s] [balancing_pool] Queued: 102 Built: 0   Failed: 0   Skipped: 0   Ignored: 0   Fetched: 0   Tobuild: 102  Time: 00:00:08
   [00:00:15] Recording filesystem state for prepkg... done
   [00:00:15] Building 102 packages using up to 16 builders
   [00:00:15] Hit CTRL+t at any time to see build progress and stats
   [00:00:15] [01] [00:00:00] Builder starting
   [00:00:19] [01] [00:00:04] Builder started
   [00:00:19] [01] [00:00:00] Building ports-mgmt/pkg | pkg-1.21.3
   [00:02:24] [01] [00:02:05] Finished ports-mgmt/pkg | pkg-1.21.3: Success
   [00:02:25] [01] [00:00:00] Building print/indexinfo | indexinfo-0.3.1
   ...
   [02:33:24] [01] [00:00:00] Building devel/git@default | git-2.46.0
   [02:41:45] [01] [00:08:21] Finished devel/git@default | git-2.46.0: Success
   [02:41:47] Stopping 16 builders
   [02:42:06] Creating pkg repository
   [02:42:06] Signing repository with key: /usr/local/etc/ssl/private/build.example.com-sk.key
   Creating repository in /tmp/packages: 100%
   Packing files for repository: 100%
   [02:42:12] Signing pkg bootstrap with method: pubkey
   [02:42:12] Committing packages to repository: /usr/local/poudriere/data/packages/141Ramd64-default-devel/.real_1723160323 via .latest symlink
   [02:42:12] Removing old packages
   [02:42:12] Built ports: ports-mgmt/pkg devel/autoconf-switch ports-mgmt/portmaster dns/public_suffix_list print/indexinfo devel/pkgconf textproc/expat2 textproc/xmlcatmgr devel/libatomic_ops security/rhash devel/libedit converters/libiconv textproc/sdocbook-xml textproc/xmlcharent textproc/iso8879 devel/gmake devel/libffi devel/libuv devel/readline security/libgpg-error www/libnghttp2 textproc/docbook-xml archivers/gtar textproc/docbook-sgml misc/getopt devel/boehm-gc devel/xxhash textproc/libyaml textproc/docbook math/mpdecimal devel/libunwind textproc/docbook-xsl devel/libunistring databases/db5 lang/perl5.36 devel/p5-Module-Build devel/p5-TimeDate converters/p5-Encode-Locale converters/p5-Text-Unidecode www/p5-HTML-Tagset lang/p5-Error security/p5-Digest-HMAC textproc/p5-Unicode-EastAsianWidth www/p5-Mozilla-CA www/p5-LWP-MediaTypes devel/p5-IO-HTML net/p5-URI devel/p5-Clone misc/help2man devel/p5-Locale-libintl www/p5-HTTP-Date security/p5-Authen-SASL net/p5-IO-Socket-IP www/p5-HTTP-Message www/p5-HTML-Parser www/p5-CGI print/texinfo dns/libidn2 devel/m4 devel/libtool devel/autoconf devel/automake print/libpaper security/libgcrypt devel/bison shells/bash devel/pcre2 security/openssl security/p5-Net-SSLeay security/p5-IO-Socket-SSL security/libssh2 www/w3m ftp/wget lang/python311 devel/py-flit-core@py311 devel/py-setuptools@py311 devel/py-installer@py311 devel/py-packaging@py311 devel/py-pyproject_hooks@py311 devel/py-build@py311 devel/py-wheel@py311 devel/ninja devel/meson@py311 archivers/liblz4 dns/libpsl devel/jsoncpp archivers/zstd ftp/curl net/rsync lang/ruby32 devel/ruby-gems textproc/rubygem-asciidoctor devel/rubygem-stringio textproc/rubygem-psych devel/rubygem-rdoc databases/ruby-bdb ports-mgmt/portupgrade devel/cmake-core textproc/libxml2 textproc/libxslt textproc/xmlto devel/git@default
   [141Ramd64-default-devel] [2024-08-08_22h56m31s] [committing] Queued: 102 Built: 102 Failed: 0   Skipped: 0   Ignored: 0   Fetched: 0   Tobuild: 0    Time: 02:42:05

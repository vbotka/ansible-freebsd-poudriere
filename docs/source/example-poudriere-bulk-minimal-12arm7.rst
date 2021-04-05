.. _ug_example_bulk_minimal_12arm7:

bulk minimal 12arm7
"""""""""""""""""""

HW and OS info ::

   [root@truenas ~]# dmesg
   ...
   FreeBSD 12.2-RELEASE-p3 7851f4a452d(HEAD) TRUENAS amd64
   FreeBSD clang version 10.0.1 (git@github.com:llvm/llvm-project.git llvmorg-10.0.1-0-gef32c611aa2)
   VT(vga): text 80x25
   CPU: Intel(R) Xeon(R) CPU           E5620  @ 2.40GHz (2399.37-MHz K8-class CPU)
   ...

VM info ::

  [admin@build ~]$ dmesg
  FreeBSD 12.2-RELEASE r366954 GENERIC amd64
  FreeBSD clang version 10.0.1 (git@github.com:llvm/llvm-project.git llvmorg-10.0.1-0-gef32c611aa2)
  VT(efifb): resolution 1024x768
  CPU: Intel(R) Xeon(R) CPU           E5620  @ 2.40GHz (2399.33-MHz K8-class CPU)
  ...
  Hypervisor: Origin = "bhyve bhyve "
  real memory  = 68717379584 (65534 MB)
  avail memory = 16618844160 (15848 MB)
  Event timer "LAPIC" quality 600
  ACPI APIC Table: <BHYVE  BVMADT  >
  FreeBSD/SMP: Multiprocessor System Detected: 16 CPUs
  FreeBSD/SMP: 1 package(s) x 4 core(s) x 4 hardware threads
  ...

VM OS info ::
  
  [admin@build ~]$ uname -a
  FreeBSD build.example.com 12.2-RELEASE FreeBSD 12.2-RELEASE r366954 GENERIC  amd64

QEMU list ::

  [root@build /usr/home/admin]# /usr/local/etc/rc.d/qemu_user_static list

  ...

  name: aarch64
  interpreter: /usr/local/bin/qemu-aarch64-static
  flags: ENABLED USE_MASK 
  magic size: 20
  magic offset: 0
  magic: 0x7f 0x45 0x4c 0x46  0x02 0x01 0x01 0x00  0x00 0x00 0x00 0x00 
         0x00 0x00 0x00 0x00  0x02 0x00 0xb7 0x00 
  mask:  0xff 0xff 0xff 0xff  0xff 0xff 0xff 0x00  0xff 0xff 0xff 0xff 
         0xff 0xff 0xff 0xff  0xfe 0xff 0xff 0xff 

  name: armv7
  interpreter: /usr/local/bin/qemu-arm-static
  flags: ENABLED USE_MASK 
  magic size: 20
  magic offset: 0
  magic: 0x7f 0x45 0x4c 0x46  0x01 0x01 0x01 0x00  0x00 0x00 0x00 0x00 
         0x00 0x00 0x00 0x00  0x02 0x00 0x28 0x00 
  mask:  0xff 0xff 0xff 0xff  0xff 0xff 0xff 0x00  0xff 0xff 0xff 0xff 
         0xff 0xff 0xff 0xff  0xfe 0xff 0xff 0xff 

  name: armv6
  interpreter: /usr/local/bin/qemu-arm-static
  flags: ENABLED USE_MASK 
  magic size: 20
  magic offset: 0
  magic: 0x7f 0x45 0x4c 0x46  0x01 0x01 0x01 0x00  0x00 0x00 0x00 0x00 
         0x00 0x00 0x00 0x00  0x02 0x00 0x28 0x00 
  mask:  0xff 0xff 0xff 0xff  0xff 0xff 0xff 0x00  0xff 0xff 0xff 0xff 
         0xff 0xff 0xff 0xff  0xfe 0xff 0xff 0xff 

  name: arm
  interpreter: /usr/local/bin/qemu-arm-static
  flags: ENABLED USE_MASK 
  magic size: 20
  magic offset: 0
  magic: 0x7f 0x45 0x4c 0x46  0x01 0x01 0x01 0x00  0x00 0x00 0x00 0x00 
         0x00 0x00 0x00 0x00  0x02 0x00 0x28 0x00 
  mask:  0xff 0xff 0xff 0xff  0xff 0xff 0xff 0x00  0xff 0xff 0xff 0xff 
         0xff 0xff 0xff 0xff  0xfe 0xff 0xff 0xff
  
Result (line 345 in the log below) ::

   [12arm7-local-devel] [2021-04-03_21h04m45s] [committing:] Queued: 158 Built: 145 Failed: 1   Skipped: 12  Ignored: 0   Tobuild: 0    Time: 16:39:35

Command and log

.. code-block:: sh
   :emphasize-lines: 1,345
   :linenos:

   [root@build /usr/home/admin]# poudriere bulk -j 12arm7 -p local -z devel -f /usr/local/etc/poudriere.d/pkglist_arm/minimal 
   [00:00:00] Cross-building ports for armv7 on amd64 requires QEMU
   [00:00:00] Creating the reference jail... done
   [00:00:15] Mounting system devices for 12arm7-local-devel
   [00:00:15] Mounting ports/packages/distfiles
   [00:00:15] Converting package repository to new format
   [00:00:15] Stashing existing package repository
   [00:00:15] Mounting packages from: /zroot/poudriere/data/packages/12arm7-local-devel
   [00:00:15] Raising MAX_EXECUTION_TIME and NOHANG_TIME for QEMU from QEMU_ values
   [00:00:15] Copying latest version of the emulator from: /usr/local/bin/qemu-arm-static
   [00:00:15] Appending to make.conf: /usr/local/etc/poudriere.d/make.conf
   /etc/resolv.conf -> /zroot/poudriere/data/.m/12arm7-local-devel/ref/etc/resolv.conf
   [00:00:15] Starting jail 12arm7-local-devel
   [00:00:50] Logs: /zroot/poudriere/data/logs/bulk/12arm7-local-devel/2021-04-03_21h04m45s
   [00:00:50] WWW: http://build.example.com//build.html?mastername=12arm7-local-devel&build=2021-04-03_21h04m45s
   [00:00:50] Loading MOVED for /zroot/poudriere/data/.m/12arm7-local-devel/ref/usr/ports
   [00:00:56] Ports supports: FLAVORS SELECTED_OPTIONS
   [00:00:56] Gathering ports metadata
   [00:01:07] Calculating ports order and dependencies
   [00:01:08] Sanity checking the repository
   [00:01:08] Checking packages for incremental rebuild needs
   [00:01:08] Deleting stale symlinks... done
   [00:01:08] Deleting empty directories... done
   [00:01:14] Cleaning the build queue
   [00:01:14] Sanity checking build queue
   [00:01:14] Processing PRIORITY_BOOST
   [00:01:15] Balancing pool
   [00:01:15] Recording filesystem state for prepkg... done
   [00:01:15] Building 158 packages using 16 builders
   [00:01:15] Starting/Cloning builders
   [00:02:29] Hit CTRL+t at any time to see build progress and stats
   [00:02:29] [01] [00:00:00] Building ports-mgmt/pkg | pkg-1.16.3
   [00:23:45] [01] [00:21:16] Finished ports-mgmt/pkg | pkg-1.16.3: Success
   [00:23:48] [01] [00:00:00] Building lang/perl5.32 | perl5-5.32.1_1
   [00:23:48] [02] [00:00:00] Building print/indexinfo | indexinfo-0.3.1
   [00:23:48] [03] [00:00:00] Building devel/pkgconf | pkgconf-1.7.4,1
   [00:23:48] [04] [00:00:00] Building converters/libiconv | libiconv-1.16
   [00:23:49] [05] [00:00:00] Building devel/autoconf-wrapper | autoconf-wrapper-20131203
   [00:23:49] [06] [00:00:00] Building textproc/xmlcatmgr | xmlcatmgr-2.2_2
   [00:23:49] [07] [00:00:00] Building textproc/expat2 | expat-2.2.10
   [00:23:49] [08] [00:00:00] Building security/rhash | rhash-1.4.1
   [00:23:49] [09] [00:00:00] Building devel/pcre | pcre-8.44
   [00:23:49] [10] [00:00:00] Building lang/tcl86 | tcl86-8.6.11_1
   [00:23:49] [11] [00:00:00] Building devel/libedit | libedit-3.1.20210216,1
   [00:23:49] [12] [00:00:00] Building devel/npth | npth-1.6
   [00:23:49] [13] [00:00:00] Building print/libpaper | libpaper-1.1.24.4
   [00:23:49] [14] [00:00:00] Building devel/cvsps | cvsps-2.1_2
   [00:23:49] [15] [00:00:00] Building ports-mgmt/portmaster | portmaster-3.19_27
   [00:24:35] [05] [00:00:46] Finished devel/autoconf-wrapper | autoconf-wrapper-20131203: Success
   [00:24:39] [15] [00:00:50] Finished ports-mgmt/portmaster | portmaster-3.19_27: Success
   [00:24:44] [02] [00:00:56] Finished print/indexinfo | indexinfo-0.3.1: Success
   [00:24:46] [02] [00:00:00] Building devel/readline | readline-8.1.0
   [00:24:46] [05] [00:00:00] Building devel/libffi | libffi-3.3_1
   [00:24:46] [15] [00:00:00] Building devel/gmake | gmake-4.3_2
   [00:24:46] [16] [00:00:00] Building security/libgpg-error | libgpg-error-1.42
   [00:26:25] [14] [00:02:36] Finished devel/cvsps | cvsps-2.1_2: Success
   [00:26:28] [14] [00:00:00] Building devel/gettext-runtime | gettext-runtime-0.21
   [00:27:41] [06] [00:03:52] Finished textproc/xmlcatmgr | xmlcatmgr-2.2_2: Success
   [00:27:44] [06] [00:00:00] Building textproc/iso8879 | iso8879-1986_3
   [00:28:34] [06] [00:00:50] Finished textproc/iso8879 | iso8879-1986_3: Success
   [00:28:37] [06] [00:00:00] Building textproc/xmlcharent | xmlcharent-0.3_2
   [00:28:39] [13] [00:04:50] Finished print/libpaper | libpaper-1.1.24.4: Success
   [00:28:42] [13] [00:00:00] Building devel/libtextstyle | libtextstyle-0.21
   [00:29:26] [06] [00:00:49] Finished textproc/xmlcharent | xmlcharent-0.3_2: Success
   [00:29:29] [06] [00:00:00] Building textproc/sdocbook-xml | sdocbook-xml-1.1_2,2
   [00:29:53] [12] [00:06:04] Finished devel/npth | npth-1.6: Success
   [00:29:55] [12] [00:00:00] Building textproc/docbook-xml | docbook-xml-5.0_3
   [00:30:17] [06] [00:00:48] Finished textproc/sdocbook-xml | sdocbook-xml-1.1_2,2: Success
   [00:30:19] [06] [00:00:00] Building textproc/docbook-sgml | docbook-sgml-4.5_1
   [00:31:19] [12] [00:01:24] Finished textproc/docbook-xml | docbook-xml-5.0_3: Success
   [00:31:23] [12] [00:00:00] Building devel/libunistring | libunistring-0.9.10_1
   [00:31:44] [06] [00:01:25] Finished textproc/docbook-sgml | docbook-sgml-4.5_1: Success
   [00:31:47] [06] [00:00:00] Building textproc/docbook | docbook-1.5
   [00:32:36] [06] [00:00:49] Finished textproc/docbook | docbook-1.5: Success
   [00:32:38] [06] [00:00:00] Building textproc/docbook-xsl | docbook-xsl-1.79.1_1,1
   [00:34:03] [05] [00:09:17] Finished devel/libffi | libffi-3.3_1: Success
   [00:34:06] [05] [00:00:00] Building archivers/gtar | gtar-1.34
   [00:34:40] [07] [00:10:51] Finished textproc/expat2 | expat-2.2.10: Success
   [00:35:08] [03] [00:11:20] Finished devel/pkgconf | pkgconf-1.7.4,1: Success
   [00:35:11] [03] [00:00:00] Building textproc/libxml2 | libxml2-2.9.10_3
   [00:35:11] [07] [00:00:00] Building www/libnghttp2 | libnghttp2-1.43.0
   [00:38:07] [08] [00:14:18] Finished security/rhash | rhash-1.4.1: Success
   [00:38:10] [08] [00:00:00] Building security/libtasn1 | libtasn1-4.16.0_1
   [00:40:19] [15] [00:15:33] Finished devel/gmake | gmake-4.3_2: Success
   [00:40:23] [15] [00:00:00] Building databases/db5 | db5-5.3.28_7
   [00:40:43] [06] [00:08:05] Finished textproc/docbook-xsl | docbook-xsl-1.79.1_1,1: Success
   [00:40:49] [06] [00:00:00] Building textproc/libyaml | libyaml-0.2.5
   [00:41:26] [11] [00:17:37] Finished devel/libedit | libedit-3.1.20210216,1: Success
   [00:41:28] [11] [00:00:00] Building devel/libltdl | libltdl-2.4.6
   [00:41:33] [16] [00:16:47] Finished security/libgpg-error | libgpg-error-1.42: Success
   [00:41:36] [16] [00:00:00] Building security/libassuan | libassuan-2.5.4
   [00:42:00] [04] [00:18:12] Finished converters/libiconv | libiconv-1.16: Success
   [00:42:03] [04] [00:00:00] Building misc/getopt | getopt-1.1.6
   [00:43:23] [04] [00:01:20] Finished misc/getopt | getopt-1.1.6: Success
   [00:43:29] [04] [00:00:00] Building devel/xxhash | xxhash-0.8.0
   [00:43:53] [02] [00:19:07] Finished devel/readline | readline-8.1.0: Success
   [00:43:56] [02] [00:00:00] Building databases/gdbm | gdbm-1.19
   [00:47:57] [04] [00:04:28] Finished devel/xxhash | xxhash-0.8.0: Success
   [00:48:57] [11] [00:07:29] Finished devel/libltdl | libltdl-2.4.6: Success
   [00:51:15] [16] [00:09:39] Finished security/libassuan | libassuan-2.5.4: Success
   [00:51:18] [04] [00:00:00] Building security/pinentry-curses | pinentry-curses-1.1.1
   [00:52:04] [06] [00:11:15] Finished textproc/libyaml | libyaml-0.2.5: Success
   [00:52:52] [07] [00:17:41] Finished www/libnghttp2 | libnghttp2-1.43.0: Success
   [00:56:33] [04] [00:05:15] Finished security/pinentry-curses | pinentry-curses-1.1.1: Success
   [00:56:35] [04] [00:00:00] Building security/pinentry | pinentry-1.1.1
   [00:57:30] [04] [00:00:55] Finished security/pinentry | pinentry-1.1.1: Success
   [00:59:15] [08] [00:21:05] Finished security/libtasn1 | libtasn1-4.16.0_1: Success
   [00:59:16] [02] [00:15:20] Finished databases/gdbm | gdbm-1.19: Success
   [01:01:39] [14] [00:35:11] Finished devel/gettext-runtime | gettext-runtime-0.21: Success
   [01:13:49] [05] [00:39:43] Finished archivers/gtar | gtar-1.34: Success
   [01:15:44] [03] [00:40:33] Finished textproc/libxml2 | libxml2-2.9.10_3: Success
   [01:18:33] [10] [00:54:44] Finished lang/tcl86 | tcl86-8.6.11_1: Success
   [01:18:36] [02] [00:00:00] Building databases/sqlite3 | sqlite3-3.34.1,1
   [01:23:13] [09] [00:59:24] Finished devel/pcre | pcre-8.44: Success
   [01:25:00] [13] [00:56:18] Finished devel/libtextstyle | libtextstyle-0.21: Success
   [01:25:03] [03] [00:00:00] Building devel/gettext-tools | gettext-tools-0.21
   [02:01:52] [12] [01:30:29] Finished devel/libunistring | libunistring-0.9.10_1: Success
   [02:01:55] [04] [00:00:00] Building dns/libidn2 | libidn2-2.3.0_1
   [02:07:11] [02] [00:48:35] Finished databases/sqlite3 | sqlite3-3.34.1,1: Success
   [02:17:34] [15] [01:37:11] Finished databases/db5 | db5-5.3.28_7: Success
   [02:18:27] [04] [00:16:32] Finished dns/libidn2 | libidn2-2.3.0_1: Success
   [02:53:23] [01] [02:29:35] Finished lang/perl5.32 | perl5-5.32.1_1: Success
   [02:53:30] [01] [00:00:00] Building security/openssl | openssl-1.1.1j_1,1
   [02:53:30] [02] [00:00:00] Building converters/p5-Text-Unidecode | p5-Text-Unidecode-1.30
   [02:53:30] [04] [00:00:00] Building textproc/p5-Unicode-EastAsianWidth | p5-Unicode-EastAsianWidth-12.0
   [02:53:30] [05] [00:00:00] Building devel/p5-Locale-libintl | p5-Locale-libintl-1.32
   [02:53:30] [06] [00:00:00] Building misc/help2man | help2man-1.48.1
   [02:53:30] [07] [00:00:00] Building devel/p5-TimeDate | p5-TimeDate-2.33,1
   [02:53:30] [08] [00:00:00] Building security/libksba | libksba-1.5.0
   [02:53:30] [09] [00:00:00] Building devel/p5-Clone | p5-Clone-0.45
   [02:53:30] [10] [00:00:00] Building converters/p5-Encode-Locale | p5-Encode-Locale-1.05
   [02:53:30] [11] [00:00:00] Building www/p5-LWP-MediaTypes | p5-LWP-MediaTypes-6.04
   [02:53:30] [12] [00:00:00] Building devel/p5-IO-HTML | p5-IO-HTML-1.001_1
   [02:53:30] [13] [00:00:00] Building net/p5-URI | p5-URI-5.07
   [02:53:30] [14] [00:00:00] Building www/p5-HTML-Tagset | p5-HTML-Tagset-3.20_1
   [02:53:30] [15] [00:00:00] Building net/p5-Socket6 | p5-Socket6-0.29
   [02:53:30] [16] [00:00:00] Building textproc/utf8proc | utf8proc-2.6.1
   [02:56:01] [04] [00:02:31] Finished textproc/p5-Unicode-EastAsianWidth | p5-Unicode-EastAsianWidth-12.0: Success
   [02:56:02] [10] [00:02:32] Finished converters/p5-Encode-Locale | p5-Encode-Locale-1.05: Success
   [02:56:02] [14] [00:02:32] Finished www/p5-HTML-Tagset | p5-HTML-Tagset-3.20_1: Success
   [02:56:03] [12] [00:02:33] Finished devel/p5-IO-HTML | p5-IO-HTML-1.001_1: Success
   [02:56:03] [04] [00:00:00] Building security/p5-Digest-HMAC | p5-Digest-HMAC-1.03_1
   [02:56:05] [11] [00:02:35] Finished www/p5-LWP-MediaTypes | p5-LWP-MediaTypes-6.04: Success
   [02:56:05] [10] [00:00:00] Building www/p5-Mozilla-CA | p5-Mozilla-CA-20200520
   [02:56:05] [14] [00:00:00] Building lang/p5-Error | p5-Error-0.17029
   [02:56:05] [12] [00:00:00] Building devel/p5-Term-ReadKey | p5-Term-ReadKey-2.38_1
   [02:56:08] [07] [00:02:38] Finished devel/p5-TimeDate | p5-TimeDate-2.33,1: Success
   [02:56:11] [07] [00:00:00] Building www/p5-HTTP-Date | p5-HTTP-Date-6.05
   [02:56:17] [13] [00:02:47] Finished net/p5-URI | p5-URI-5.07: Success
   [02:56:20] [16] [00:02:50] Finished textproc/utf8proc | utf8proc-2.6.1: Success
   [02:56:24] [09] [00:02:54] Finished devel/p5-Clone | p5-Clone-0.45: Success
   [02:56:34] [02] [00:03:04] Finished converters/p5-Text-Unidecode | p5-Text-Unidecode-1.30: Success
   [02:56:50] [06] [00:03:20] Finished misc/help2man | help2man-1.48.1: Success
   [02:57:48] [05] [00:04:18] Finished devel/p5-Locale-libintl | p5-Locale-libintl-1.32: Success
   [02:57:50] [02] [00:00:00] Building print/texinfo | texinfo-6.7_4,1
   [02:57:58] [04] [00:01:55] Finished security/p5-Digest-HMAC | p5-Digest-HMAC-1.03_1: Success
   [02:57:59] [10] [00:01:54] Finished www/p5-Mozilla-CA | p5-Mozilla-CA-20200520: Success
   [02:58:00] [04] [00:00:00] Building security/p5-Authen-SASL | p5-Authen-SASL-2.16_1
   [02:58:04] [14] [00:01:59] Finished lang/p5-Error | p5-Error-0.17029: Success
   [02:58:07] [15] [00:04:37] Finished net/p5-Socket6 | p5-Socket6-0.29: Success
   [02:58:09] [05] [00:00:00] Building net/p5-IO-Socket-INET6 | p5-IO-Socket-INET6-2.72_1
   [02:58:10] [07] [00:01:59] Finished www/p5-HTTP-Date | p5-HTTP-Date-6.05: Success
   [02:58:12] [06] [00:00:00] Building www/p5-HTTP-Message | p5-HTTP-Message-6.28
   [02:58:24] [12] [00:02:19] Finished devel/p5-Term-ReadKey | p5-Term-ReadKey-2.38_1: Success
   [02:59:42] [05] [00:01:33] Finished net/p5-IO-Socket-INET6 | p5-IO-Socket-INET6-2.72_1: Success
   [02:59:43] [04] [00:01:43] Finished security/p5-Authen-SASL | p5-Authen-SASL-2.16_1: Success
   [03:00:05] [06] [00:01:53] Finished www/p5-HTTP-Message | p5-HTTP-Message-6.28: Success
   [03:00:07] [04] [00:00:00] Building www/p5-HTML-Parser | p5-HTML-Parser-3.75
   [03:02:13] [04] [00:02:06] Finished www/p5-HTML-Parser | p5-HTML-Parser-3.75: Success
   [03:02:14] [04] [00:00:00] Building www/p5-CGI | p5-CGI-4.51
   [03:03:47] [04] [00:01:33] Finished www/p5-CGI | p5-CGI-4.51: Success
   [03:07:57] [08] [00:14:27] Finished security/libksba | libksba-1.5.0: Success
   [03:22:59] [02] [00:25:09] Finished print/texinfo | texinfo-6.7_4,1: Success
   [03:23:02] [02] [00:00:00] Building devel/m4 | m4-1.4.18_1,1
   [03:23:02] [04] [00:00:00] Building security/libgcrypt | libgcrypt-1.9.2_1
   [03:23:02] [05] [00:00:00] Building math/gmp | gmp-6.2.1
   [03:42:04] [02] [00:19:02] Finished devel/m4 | m4-1.4.18_1,1: Success
   [03:42:06] [02] [00:00:00] Building devel/autoconf | autoconf-2.69_3
   [03:42:06] [06] [00:00:00] Building devel/libtool | libtool-2.4.6_1
   [03:42:06] [07] [00:00:00] Building devel/bison | bison-3.7.5,1
   [03:48:13] [02] [00:06:07] Finished devel/autoconf | autoconf-2.69_3: Success
   [03:48:15] [02] [00:00:00] Building devel/automake | automake-1.16.3
   [03:49:45] [06] [00:07:39] Finished devel/libtool | libtool-2.4.6_1: Success
   [03:52:00] [02] [00:03:45] Finished devel/automake | automake-1.16.3: Success
   [03:52:01] [02] [00:00:00] Building devel/libuv | libuv-1.41.0
   [03:52:01] [06] [00:00:00] Building devel/libatomic_ops | libatomic_ops-7.6.10
   [03:52:01] [08] [00:00:00] Building devel/pcre2 | pcre2-10.36
   [03:57:06] [03] [02:32:03] Finished devel/gettext-tools | gettext-tools-0.21: Success
   [03:58:04] [06] [00:06:03] Finished devel/libatomic_ops | libatomic_ops-7.6.10: Success
   [03:58:06] [03] [00:00:00] Building devel/boehm-gc | boehm-gc-8.0.4_1
   [03:59:18] [04] [00:36:16] Finished security/libgcrypt | libgcrypt-1.9.2_1: Failed: build
   [03:59:20] [04] [00:36:18] Skipping devel/git | git-2.31.0: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping devel/glib20 | glib-2.66.7_1,1: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping security/gnupg | gnupg-2.2.27: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping security/gnutls | gnutls-3.6.15: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping textproc/gtk-doc | gtk-doc-1.33.2: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping textproc/libxslt | libxslt-1.1.34_1: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping security/p11-kit | p11-kit-0.23.22_1: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping devel/p5-subversion | p5-subversion-1.14.1: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping devel/subversion | subversion-1.14.1: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping textproc/xmlto | xmlto-0.0.28: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping textproc/yelp-tools | yelp-tools-3.38.0: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [03:59:20] [04] [00:36:18] Skipping textproc/yelp-xsl | yelp-xsl-3.38.3: Dependent port security/libgcrypt | libgcrypt-1.9.2_1 failed
   [04:07:41] [03] [00:09:35] Finished devel/boehm-gc | boehm-gc-8.0.4_1: Success
   [04:12:27] [02] [00:20:26] Finished devel/libuv | libuv-1.41.0: Success
   [04:12:50] [07] [00:30:44] Finished devel/bison | bison-3.7.5,1: Success
   [04:12:52] [02] [00:00:00] Building shells/bash | bash-5.1.4_1
   [04:40:07] [08] [00:48:06] Finished devel/pcre2 | pcre2-10.36: Success
   [04:44:41] [02] [00:31:49] Finished shells/bash | bash-5.1.4_1: Success
   [04:44:44] [02] [00:00:00] Building shells/bash-completion | bash-completion-2.11,2
   [04:49:35] [02] [00:04:51] Finished shells/bash-completion | bash-completion-2.11,2: Success
   [04:57:06] [05] [01:34:04] Finished math/gmp | gmp-6.2.1: Success
   [04:57:09] [02] [00:00:00] Building security/nettle | nettle-3.6
   [05:07:59] [01] [02:14:29] Finished security/openssl | openssl-1.1.1j_1,1: Success
   [05:08:05] [01] [00:00:00] Building lang/python37 | python37-3.7.10
   [05:08:05] [03] [00:00:00] Building security/ca_root_nss | ca_root_nss-3.63
   [05:08:05] [04] [00:00:00] Building lang/ruby27 | ruby-2.7.2_1,1
   [05:08:05] [05] [00:00:00] Building devel/apr1 | apr-1.7.0.1.6.1_1
   [05:08:05] [06] [00:00:00] Building www/w3m | w3m-0.5.3.20210306
   [05:08:05] [07] [00:00:00] Building security/p5-Net-SSLeay | p5-Net-SSLeay-1.88
   [05:08:05] [08] [00:00:00] Building ftp/wget | wget-1.21
   [05:10:25] [03] [00:02:20] Finished security/ca_root_nss | ca_root_nss-3.63: Success
   [05:10:27] [03] [00:00:00] Building ftp/curl | curl-7.75.0
   [05:13:15] [07] [00:05:10] Finished security/p5-Net-SSLeay | p5-Net-SSLeay-1.88: Success
   [05:13:17] [07] [00:00:00] Building security/p5-IO-Socket-SSL | p5-IO-Socket-SSL-2.070
   [05:15:18] [07] [00:02:01] Finished security/p5-IO-Socket-SSL | p5-IO-Socket-SSL-2.070: Success
   [05:24:15] [06] [00:16:10] Finished www/w3m | w3m-0.5.3.20210306: Success
   [05:29:19] [02] [00:32:10] Finished security/nettle | nettle-3.6: Success
   [05:39:51] [08] [00:31:46] Finished ftp/wget | wget-1.21: Success
   [06:01:19] [03] [00:50:52] Finished ftp/curl | curl-7.75.0: Success
   [06:08:04] [05] [00:59:59] Finished devel/apr1 | apr-1.7.0.1.6.1_1: Success
   [06:22:20] [01] [01:14:15] Finished lang/python37 | python37-3.7.10: Success
   [06:22:25] [01] [00:00:00] Building devel/py-setuptools@py37 | py37-setuptools-44.0.0
   [06:22:25] [02] [00:00:00] Building devel/ninja | ninja-1.10.2,2
   [06:23:57] [01] [00:01:32] Finished devel/py-setuptools@py37 | py37-setuptools-44.0.0: Success
   [06:24:01] [01] [00:00:00] Building devel/py-pycparser@py37 | py37-pycparser-2.20
   [06:24:01] [03] [00:00:00] Building devel/py-six@py37 | py37-six-1.15.0
   [06:24:01] [05] [00:00:00] Building devel/py-pytz@py37 | py37-pytz-2020.5,1
   [06:24:01] [06] [00:00:00] Building net/py-pysocks@py37 | py37-pysocks-1.7.1
   [06:24:01] [07] [00:00:00] Building security/py-certifi@py37 | py37-certifi-2020.12.5
   [06:24:01] [08] [00:00:00] Building dns/py-idna@py37 | py37-idna-2.10
   [06:24:01] [09] [00:00:00] Building lang/cython@py37 | py37-cython-0.29.21
   [06:24:01] [10] [00:00:00] Building textproc/py-chardet@py37 | py37-chardet-3.0.4_3,1
   [06:24:01] [11] [00:00:00] Building textproc/py-libxml2@py37 | py37-libxml2-2.9.10_3
   [06:24:01] [12] [00:00:00] Building devel/py-pyparsing@py37 | py37-pyparsing-2.4.7
   [06:24:01] [13] [00:00:00] Building textproc/py-markupsafe@py37 | py37-markupsafe-1.1.1_1
   [06:24:01] [14] [00:00:00] Building textproc/py-alabaster@py37 | py37-alabaster-0.7.6
   [06:24:01] [15] [00:00:00] Building textproc/py-docutils@py37 | py37-docutils-0.16
   [06:24:01] [16] [00:00:00] Building textproc/py-sphinxcontrib-devhelp@py37 | py37-sphinxcontrib-devhelp-1.0.2
   [06:26:35] [14] [00:02:34] Finished textproc/py-alabaster@py37 | py37-alabaster-0.7.6: Success
   [06:26:39] [03] [00:02:38] Finished devel/py-six@py37 | py37-six-1.15.0: Success
   [06:26:39] [16] [00:02:38] Finished textproc/py-sphinxcontrib-devhelp@py37 | py37-sphinxcontrib-devhelp-1.0.2: Success
   [06:26:40] [06] [00:02:39] Finished net/py-pysocks@py37 | py37-pysocks-1.7.1: Success
   [06:26:40] [07] [00:02:39] Finished security/py-certifi@py37 | py37-certifi-2020.12.5: Success
   [06:26:43] [14] [00:00:00] Building textproc/py-sphinxcontrib-qthelp@py37 | py37-sphinxcontrib-qthelp-1.0.3
   [06:26:44] [12] [00:02:43] Finished devel/py-pyparsing@py37 | py37-pyparsing-2.4.7: Success
   [06:26:45] [08] [00:02:44] Finished dns/py-idna@py37 | py37-idna-2.10: Success
   [06:26:47] [03] [00:00:00] Building textproc/py-pygments@py37 | py37-pygments-2.7.2
   [06:26:47] [16] [00:00:00] Building graphics/py-imagesize@py37 | py37-imagesize-1.1.0
   [06:26:47] [06] [00:00:00] Building textproc/py-sphinxcontrib-htmlhelp@py37 | py37-sphinxcontrib-htmlhelp-1.0.3
   [06:26:48] [07] [00:00:00] Building textproc/py-sphinxcontrib-jsmath@py37 | py37-sphinxcontrib-jsmath-1.0.1
   [06:26:48] [13] [00:02:47] Finished textproc/py-markupsafe@py37 | py37-markupsafe-1.1.1_1: Success
   [06:26:50] [10] [00:02:49] Finished textproc/py-chardet@py37 | py37-chardet-3.0.4_3,1: Success
   [06:26:52] [01] [00:02:51] Finished devel/py-pycparser@py37 | py37-pycparser-2.20: Success
   [06:26:53] [12] [00:00:00] Building textproc/py-sphinxcontrib-applehelp@py37 | py37-sphinxcontrib-applehelp-1.0.2
   [06:26:54] [08] [00:00:00] Building devel/py-packaging@py37 | py37-packaging-20.9
   [06:26:56] [05] [00:02:55] Finished devel/py-pytz@py37 | py37-pytz-2020.5,1: Success
   [06:26:57] [13] [00:00:00] Building textproc/py-sphinxcontrib-serializinghtml@py37 | py37-sphinxcontrib-serializinghtml-1.1.4
   [06:27:00] [10] [00:00:00] Building devel/scons@py37 | scons-py37-3.1.2
   [06:27:03] [01] [00:00:00] Building devel/py-cffi@py37 | py37-cffi-1.14.5
   [06:27:08] [05] [00:00:00] Building devel/py-babel@py37 | py37-Babel-2.9.0
   [06:27:40] [15] [00:03:39] Finished textproc/py-docutils@py37 | py37-docutils-0.16: Success
   [06:29:03] [14] [00:02:20] Finished textproc/py-sphinxcontrib-qthelp@py37 | py37-sphinxcontrib-qthelp-1.0.3: Success
   [06:29:12] [16] [00:02:25] Finished graphics/py-imagesize@py37 | py37-imagesize-1.1.0: Success
   [06:29:14] [07] [00:02:26] Finished textproc/py-sphinxcontrib-jsmath@py37 | py37-sphinxcontrib-jsmath-1.0.1: Success
   [06:29:18] [06] [00:02:31] Finished textproc/py-sphinxcontrib-htmlhelp@py37 | py37-sphinxcontrib-htmlhelp-1.0.3: Success
   [06:29:24] [12] [00:02:31] Finished textproc/py-sphinxcontrib-applehelp@py37 | py37-sphinxcontrib-applehelp-1.0.2: Success
   [06:29:25] [13] [00:02:28] Finished textproc/py-sphinxcontrib-serializinghtml@py37 | py37-sphinxcontrib-serializinghtml-1.1.4: Success
   [06:29:28] [08] [00:02:34] Finished devel/py-packaging@py37 | py37-packaging-20.9: Success
   [06:29:59] [10] [00:02:59] Finished devel/scons@py37 | scons-py37-3.1.2: Success
   [06:29:59] [03] [00:03:12] Finished textproc/py-pygments@py37 | py37-pygments-2.7.2: Success
   [06:30:04] [06] [00:00:00] Building www/serf | serf-1.3.9_6
   [06:30:43] [01] [00:03:40] Finished devel/py-cffi@py37 | py37-cffi-1.14.5: Success
   [06:30:48] [01] [00:00:00] Building security/py-cryptography@py37 | py37-cryptography-3.3.2
   [06:31:19] [05] [00:04:11] Finished devel/py-babel@py37 | py37-Babel-2.9.0: Success
   [06:31:24] [03] [00:00:00] Building devel/py-Jinja2@py37 | py37-Jinja2-2.11.2_1
   [06:33:01] [03] [00:01:37] Finished devel/py-Jinja2@py37 | py37-Jinja2-2.11.2_1: Success
   [06:33:13] [11] [00:09:12] Finished textproc/py-libxml2@py37 | py37-libxml2-2.9.10_3: Success
   [06:33:18] [03] [00:00:00] Building textproc/itstool | itstool-2.0.6
   [06:34:57] [03] [00:01:39] Finished textproc/itstool | itstool-2.0.6: Success
   [06:37:18] [06] [00:07:14] Finished www/serf | serf-1.3.9_6: Success
   [06:37:51] [01] [00:07:03] Finished security/py-cryptography@py37 | py37-cryptography-3.3.2: Success
   [06:37:56] [01] [00:00:00] Building security/py-openssl@py37 | py37-openssl-20.0.1
   [06:38:05] [02] [00:15:40] Finished devel/ninja | ninja-1.10.2,2: Success
   [06:38:10] [02] [00:00:00] Building devel/meson | meson-0.57.1
   [06:39:17] [01] [00:01:21] Finished security/py-openssl@py37 | py37-openssl-20.0.1: Success
   [06:39:21] [01] [00:00:00] Building net/py-urllib3@py37 | py37-urllib3-1.25.11,1
   [06:40:07] [02] [00:01:57] Finished devel/meson | meson-0.57.1: Success
   [06:40:14] [02] [00:00:00] Building archivers/liblz4 | liblz4-1.9.3,1
   [06:40:14] [03] [00:00:00] Building devel/jsoncpp | jsoncpp-1.9.4
   [06:40:58] [01] [00:01:37] Finished net/py-urllib3@py37 | py37-urllib3-1.25.11,1: Success
   [06:41:04] [01] [00:00:00] Building www/py-requests@py37 | py37-requests-2.22.0_2
   [06:42:32] [01] [00:01:28] Finished www/py-requests@py37 | py37-requests-2.22.0_2: Success
   [06:44:41] [02] [00:04:27] Finished archivers/liblz4 | liblz4-1.9.3,1: Success
   [06:44:45] [01] [00:00:00] Building archivers/libarchive | libarchive-3.5.1,1
   [06:44:45] [02] [00:00:00] Building archivers/zstd | zstd-1.4.8
   [06:46:32] [09] [00:22:31] Finished lang/cython@py37 | py37-cython-0.29.21: Success
   [06:46:37] [05] [00:00:00] Building textproc/py-pystemmer@py37 | py37-pystemmer-2.0.0.1
   [06:48:39] [03] [00:08:25] Finished devel/jsoncpp | jsoncpp-1.9.4: Success
   [06:50:55] [05] [00:04:18] Finished textproc/py-pystemmer@py37 | py37-pystemmer-2.0.0.1: Success
   [06:50:59] [03] [00:00:00] Building textproc/py-snowballstemmer@py37 | py37-snowballstemmer-1.2.1
   [06:52:21] [03] [00:01:22] Finished textproc/py-snowballstemmer@py37 | py37-snowballstemmer-1.2.1: Success
   [06:52:26] [03] [00:00:00] Building textproc/py-sphinx@py37 | py37-sphinx-3.5.2,1
   [06:55:31] [03] [00:03:05] Finished textproc/py-sphinx@py37 | py37-sphinx-3.5.2,1: Success
   [07:00:16] [02] [00:15:31] Finished archivers/zstd | zstd-1.4.8: Success
   [07:00:21] [02] [00:00:00] Building net/rsync | rsync-3.2.3
   [07:15:27] [02] [00:15:06] Finished net/rsync | rsync-3.2.3: Success
   [07:30:49] [01] [00:46:04] Finished archivers/libarchive | libarchive-3.5.1,1: Success
   [07:30:51] [01] [00:00:00] Building devel/cmake | cmake-3.19.6
   [07:52:13] [04] [02:44:08] Finished lang/ruby27 | ruby-2.7.2_1,1: Success
   [07:52:23] [02] [00:00:00] Building devel/ruby-gems | ruby27-gems-3.0.8
   [07:53:27] [02] [00:01:04] Finished devel/ruby-gems | ruby27-gems-3.0.8: Success
   [07:53:29] [02] [00:00:00] Building devel/rubygem-rdoc | rubygem-rdoc-6.3.0
   [07:53:29] [03] [00:00:00] Building textproc/rubygem-asciidoctor | rubygem-asciidoctor-2.0.12
   [07:54:52] [03] [00:01:23] Finished textproc/rubygem-asciidoctor | rubygem-asciidoctor-2.0.12: Success
   [07:54:57] [02] [00:01:28] Finished devel/rubygem-rdoc | rubygem-rdoc-6.3.0: Success
   [07:54:59] [02] [00:00:00] Building databases/ruby-bdb | ruby27-bdb-0.6.6_8
   [08:24:12] [02] [00:29:13] Finished databases/ruby-bdb | ruby27-bdb-0.6.6_8: Success
   [08:24:14] [02] [00:00:00] Building ports-mgmt/portupgrade | portupgrade-2.4.16,2
   [08:26:32] [02] [00:02:18] Finished ports-mgmt/portupgrade | portupgrade-2.4.16,2: Success
   [15:01:07] [01] [07:30:16] Finished devel/cmake | cmake-3.19.6: Success
   [15:01:17] [01] [00:00:00] Building emulators/tpm-emulator | tpm-emulator-0.7.4_2
   [15:08:01] [01] [00:06:44] Finished emulators/tpm-emulator | tpm-emulator-0.7.4_2: Success
   [15:08:03] [01] [00:00:00] Building security/trousers | trousers-0.3.14_3
   [16:38:49] [01] [01:30:46] Finished security/trousers | trousers-0.3.14_3: Success
   [16:38:52] Stopping 16 builders
   [16:40:24] Creating pkg repository
   Creating repository in /tmp/packages: 100%
   Packing files for repository: 100%
   [16:40:25] Committing packages to repository: /zroot/poudriere/data/packages/12arm7-local-devel/.real_1617536710 via .latest symlink
   [16:40:25] Removing old packages
   [16:40:25] Built ports: ports-mgmt/pkg devel/autoconf-wrapper ports-mgmt/portmaster print/indexinfo devel/cvsps textproc/xmlcatmgr textproc/iso8879 print/libpaper textproc/xmlcharent devel/npth textproc/sdocbook-xml textproc/docbook-xml textproc/docbook-sgml textproc/docbook devel/libffi textproc/expat2 devel/pkgconf security/rhash devel/gmake textproc/docbook-xsl devel/libedit security/libgpg-error converters/libiconv misc/getopt devel/readline devel/xxhash devel/libltdl security/libassuan textproc/libyaml www/libnghttp2 security/pinentry-curses security/pinentry security/libtasn1 databases/gdbm devel/gettext-runtime archivers/gtar textproc/libxml2 lang/tcl86 devel/pcre devel/libtextstyle devel/libunistring databases/sqlite3 databases/db5 dns/libidn2 lang/perl5.32 textproc/p5-Unicode-EastAsianWidth converters/p5-Encode-Locale www/p5-HTML-Tagset devel/p5-IO-HTML www/p5-LWP-MediaTypes devel/p5-TimeDate net/p5-URI textproc/utf8proc devel/p5-Clone converters/p5-Text-Unidecode misc/help2man devel/p5-Locale-libintl security/p5-Digest-HMAC www/p5-Mozilla-CA lang/p5-Error net/p5-Socket6 www/p5-HTTP-Date devel/p5-Term-ReadKey net/p5-IO-Socket-INET6 security/p5-Authen-SASL www/p5-HTTP-Message www/p5-HTML-Parser www/p5-CGI security/libksba print/texinfo devel/m4 devel/autoconf devel/libtool devel/automake devel/gettext-tools devel/libatomic_ops devel/boehm-gc devel/libuv devel/bison devel/pcre2 shells/bash shells/bash-completion math/gmp security/openssl security/ca_root_nss security/p5-Net-SSLeay security/p5-IO-Socket-SSL www/w3m security/nettle ftp/wget ftp/curl devel/apr1 lang/python37 devel/py-setuptools textproc/py-alabaster devel/py-six textproc/py-sphinxcontrib-devhelp net/py-pysocks security/py-certifi devel/py-pyparsing dns/py-idna textproc/py-markupsafe textproc/py-chardet devel/py-pycparser devel/py-pytz textproc/py-docutils textproc/py-sphinxcontrib-qthelp graphics/py-imagesize textproc/py-sphinxcontrib-jsmath textproc/py-sphinxcontrib-htmlhelp textproc/py-sphinxcontrib-applehelp textproc/py-sphinxcontrib-serializinghtml devel/py-packaging devel/scons textproc/py-pygments devel/py-cffi devel/py-babel devel/py-Jinja2 textproc/py-libxml2 textproc/itstool www/serf security/py-cryptography devel/ninja security/py-openssl devel/meson net/py-urllib3 www/py-requests archivers/liblz4 lang/cython devel/jsoncpp textproc/py-pystemmer textproc/py-snowballstemmer textproc/py-sphinx archivers/zstd net/rsync archivers/libarchive lang/ruby27 devel/ruby-gems textproc/rubygem-asciidoctor devel/rubygem-rdoc databases/ruby-bdb ports-mgmt/portupgrade devel/cmake emulators/tpm-emulator security/trousers
   [16:40:25] Failed ports: security/libgcrypt:build
   [16:40:25] Skipped ports: devel/git devel/glib20 devel/p5-subversion devel/subversion security/gnupg security/gnutls security/p11-kit textproc/gtk-doc textproc/libxslt textproc/xmlto textproc/yelp-tools textproc/yelp-xsl
   [12arm7-local-devel] [2021-04-03_21h04m45s] [committing:] Queued: 158 Built: 145 Failed: 1   Skipped: 12  Ignored: 0   Tobuild: 0    Time: 16:39:35
   [16:40:25] Logs: /zroot/poudriere/data/logs/bulk/12arm7-local-devel/2021-04-03_21h04m45s
   [16:40:25] WWW: http://build.example.com//build.html?mastername=12arm7-local-devel&build=2021-04-03_21h04m45s
   [16:40:25] Cleaning up
   [16:40:25] Unmounting file systems

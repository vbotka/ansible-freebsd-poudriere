.. _ug_example_bulk_minimal:

Build bulk minimal
==================

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
   
Result (line 354 in the log below) ::

   [12amd64-local-devel] [2021-03-22_22h42m18s] [committing:] Queued: 160 Built: 158 Failed: 1   Skipped: 1   Ignored: 0   Tobuild: 0    Time: 01:52:20

Command and log

.. code-block:: sh
   :emphasize-lines: 1,354
   :linenos:

   [root@build /usr/home/admin]# poudriere bulk -j 12amd64 -p local -z devel -f /usr/local/etc/poudriere.d/pkglist_amd64/minimal
   [00:00:01] Creating the reference jail... done
   [00:00:09] Mounting system devices for 12amd64-local-devel
   [00:00:09] Mounting ports/packages/distfiles
   [00:00:09] Converting package repository to new format
   [00:00:09] Stashing existing package repository
   [00:00:09] Mounting packages from: /zroot/poudriere/data/packages/12amd64-local-devel
   /etc/resolv.conf -> /zroot/poudriere/data/.m/12amd64-local-devel/ref/etc/resolv.conf
   [00:00:09] Starting jail 12amd64-local-devel
   [00:00:10] Logs: /zroot/poudriere/data/logs/bulk/12amd64-local-devel/2021-03-22_22h42m18s
   [00:00:10] WWW: http://build.example.com//build.html?mastername=12amd64-local-devel&build=2021-03-22_22h42m18s
   [00:00:10] Loading MOVED for /zroot/poudriere/data/.m/12amd64-local-devel/ref/usr/ports
   [00:00:16] Ports supports: FLAVORS SELECTED_OPTIONS
   [00:00:16] Gathering ports metadata
   [00:00:19] Calculating ports order and dependencies
   [00:00:19] pkg package missing, skipping sanity
   [00:00:19] Skipping incremental rebuild and repository sanity checks
   [00:00:25] Cleaning the build queue
   [00:00:26] Sanity checking build queue
   [00:00:26] Processing PRIORITY_BOOST
   [00:00:26] Balancing pool
   [00:00:26] Recording filesystem state for prepkg... done
   [00:00:26] Building 160 packages using 16 builders
   [00:00:26] Starting/Cloning builders
   [00:01:26] Hit CTRL+t at any time to see build progress and stats
   [00:01:26] [01] [00:00:00] Building ports-mgmt/pkg | pkg-1.16.3
   [00:03:30] [01] [00:02:04] Finished ports-mgmt/pkg | pkg-1.16.3: Success
   [00:03:30] [01] [00:00:00] Building print/indexinfo | indexinfo-0.3.1
   [00:03:30] [02] [00:00:00] Building devel/pkgconf | pkgconf-1.7.4,1
   [00:03:30] [03] [00:00:00] Building lang/perl5.32 | perl5-5.32.1_1
   [00:03:30] [04] [00:00:00] Building converters/libiconv | libiconv-1.16
   [00:03:30] [05] [00:00:00] Building textproc/xmlcatmgr | xmlcatmgr-2.2_2
   [00:03:30] [06] [00:00:00] Building devel/autoconf-wrapper | autoconf-wrapper-20131203
   [00:03:30] [07] [00:00:00] Building textproc/expat2 | expat-2.2.10
   [00:03:30] [08] [00:00:00] Building devel/pcre | pcre-8.44
   [00:03:30] [09] [00:00:00] Building lang/tcl86 | tcl86-8.6.11_1
   [00:03:30] [10] [00:00:00] Building devel/libedit | libedit-3.1.20191231,1
   [00:03:30] [11] [00:00:00] Building devel/npth | npth-1.6
   [00:03:31] [12] [00:00:00] Building print/libpaper | libpaper-1.1.24.4
   [00:03:31] [13] [00:00:00] Building devel/cvsps | cvsps-2.1_2
   [00:03:31] [14] [00:00:00] Building ports-mgmt/portmaster | portmaster-3.19_27
   [00:03:42] [06] [00:00:12] Finished devel/autoconf-wrapper | autoconf-wrapper-20131203: Success
   [00:03:42] [01] [00:00:12] Finished print/indexinfo | indexinfo-0.3.1: Success
   [00:03:43] [06] [00:00:00] Building devel/libunistring | libunistring-0.9.10_1
   [00:03:43] [15] [00:00:00] Building devel/gettext-runtime | gettext-runtime-0.21
   [00:03:43] [16] [00:00:00] Building devel/libtextstyle | libtextstyle-0.21
   [00:03:43] [01] [00:00:00] Building devel/libffi | libffi-3.3_1
   [00:03:44] [14] [00:00:13] Finished ports-mgmt/portmaster | portmaster-3.19_27: Success
   [00:03:45] [14] [00:00:00] Building devel/readline | readline-8.1.0
   [00:03:51] [13] [00:00:20] Finished devel/cvsps | cvsps-2.1_2: Success
   [00:03:57] [05] [00:00:27] Finished textproc/xmlcatmgr | xmlcatmgr-2.2_2: Success
   [00:03:57] [05] [00:00:00] Building textproc/iso8879 | iso8879-1986_3
   [00:03:58] [13] [00:00:01] Building textproc/xmlcharent | xmlcharent-0.3_2
   [00:03:59] [12] [00:00:28] Finished print/libpaper | libpaper-1.1.24.4: Success
   [00:04:00] [12] [00:00:00] Building textproc/sdocbook-xml | sdocbook-xml-1.1_2,2
   [00:04:01] [11] [00:00:31] Finished devel/npth | npth-1.6: Success
   [00:04:04] [13] [00:00:07] Finished textproc/xmlcharent | xmlcharent-0.3_2: Success
   [00:04:04] [05] [00:00:07] Finished textproc/iso8879 | iso8879-1986_3: Success
   [00:04:05] [11] [00:00:01] Building textproc/docbook-xml | docbook-xml-5.0_3
   [00:04:05] [05] [00:00:00] Building textproc/docbook-sgml | docbook-sgml-4.5_1
   [00:04:06] [12] [00:00:06] Finished textproc/sdocbook-xml | sdocbook-xml-1.1_2,2: Success
   [00:04:14] [05] [00:00:09] Finished textproc/docbook-sgml | docbook-sgml-4.5_1: Success
   [00:04:15] [11] [00:00:11] Finished textproc/docbook-xml | docbook-xml-5.0_3: Success
   [00:04:16] [05] [00:00:00] Building textproc/docbook | docbook-1.5
   [00:04:17] [01] [00:00:34] Finished devel/libffi | libffi-3.3_1: Success
   [00:04:19] [02] [00:00:49] Finished devel/pkgconf | pkgconf-1.7.4,1: Success
   [00:04:19] [01] [00:00:00] Building textproc/libxml2 | libxml2-2.9.10_3
   [00:04:19] [02] [00:00:00] Building www/libnghttp2 | libnghttp2-1.43.0
   [00:04:19] [11] [00:00:00] Building security/libtasn1 | libtasn1-4.16.0_1
   [00:04:19] [12] [00:00:00] Building devel/libunwind | libunwind-20201110
   [00:04:22] [05] [00:00:06] Finished textproc/docbook | docbook-1.5: Success
   [00:04:23] [05] [00:00:00] Building textproc/docbook-xsl | docbook-xsl-1.79.1_1,1
   [00:04:23] [07] [00:00:53] Finished textproc/expat2 | expat-2.2.10: Success
   [00:04:33] [10] [00:01:03] Finished devel/libedit | libedit-3.1.20191231,1: Success
   [00:04:43] [14] [00:00:58] Finished devel/readline | readline-8.1.0: Success
   [00:04:48] [04] [00:01:18] Finished converters/libiconv | libiconv-1.16: Success
   [00:05:05] [11] [00:00:46] Finished security/libtasn1 | libtasn1-4.16.0_1: Success
   [00:05:08] [02] [00:00:49] Finished www/libnghttp2 | libnghttp2-1.43.0: Success
   [00:05:25] [15] [00:01:42] Finished devel/gettext-runtime | gettext-runtime-0.21: Success
   [00:05:26] [02] [00:00:00] Building devel/gmake | gmake-4.3_2
   [00:05:26] [04] [00:00:00] Building archivers/gtar | gtar-1.34
   [00:05:26] [05] [00:01:03] Finished textproc/docbook-xsl | docbook-xsl-1.79.1_1,1: Success
   [00:05:42] [12] [00:01:23] Finished devel/libunwind | libunwind-20201110: Success
   [00:05:59] [02] [00:00:33] Finished devel/gmake | gmake-4.3_2: Success
   [00:05:59] [02] [00:00:00] Building textproc/libyaml | libyaml-0.2.5
   [00:05:59] [05] [00:00:00] Building devel/libltdl | libltdl-2.4.6
   [00:05:59] [07] [00:00:00] Building databases/db5 | db5-5.3.28_7
   [00:05:59] [10] [00:00:00] Building devel/xxhash | xxhash-0.8.0
   [00:06:20] [10] [00:00:21] Finished devel/xxhash | xxhash-0.8.0: Success
   [00:06:22] [05] [00:00:23] Finished devel/libltdl | libltdl-2.4.6: Success
   [00:06:33] [02] [00:00:34] Finished textproc/libyaml | libyaml-0.2.5: Success
   [00:06:49] [16] [00:03:06] Finished devel/libtextstyle | libtextstyle-0.21: Success
   [00:06:51] [02] [00:00:00] Building devel/gettext-tools | gettext-tools-0.21
   [00:07:02] [04] [00:01:36] Finished archivers/gtar | gtar-1.34: Success
   [00:07:09] [09] [00:03:39] Finished lang/tcl86 | tcl86-8.6.11_1: Success
   [00:07:10] [04] [00:00:00] Building databases/sqlite3 | sqlite3-3.34.1,1
   [00:07:14] [01] [00:02:55] Finished textproc/libxml2 | libxml2-2.9.10_3: Success
   [00:07:57] [06] [00:04:14] Finished devel/libunistring | libunistring-0.9.10_1: Success
   [00:07:58] [01] [00:00:00] Building dns/libidn2 | libidn2-2.3.0_1
   [00:08:35] [01] [00:00:37] Finished dns/libidn2 | libidn2-2.3.0_1: Success
   [00:08:59] [08] [00:05:29] Finished devel/pcre | pcre-8.44: Success
   [00:12:13] [07] [00:06:14] Finished databases/db5 | db5-5.3.28_7: Success
   [00:12:16] [04] [00:05:06] Finished databases/sqlite3 | sqlite3-3.34.1,1: Success
   [00:14:10] [02] [00:07:19] Finished devel/gettext-tools | gettext-tools-0.21: Success
   [00:14:12] [01] [00:00:00] Building lang/python37 | python37-3.7.10
   [00:14:12] [02] [00:00:00] Building security/libgpg-error | libgpg-error-1.41
   [00:14:12] [04] [00:00:00] Building security/rhash | rhash-1.4.1
   [00:14:12] [05] [00:00:00] Building databases/gdbm | gdbm-1.19
   [00:14:12] [06] [00:00:00] Building misc/getopt | getopt-1.1.6
   [00:14:22] [06] [00:00:10] Finished misc/getopt | getopt-1.1.6: Success
   [00:14:45] [04] [00:00:33] Finished security/rhash | rhash-1.4.1: Success
   [00:14:46] [05] [00:00:34] Finished databases/gdbm | gdbm-1.19: Success
   [00:14:46] [04] [00:00:00] Building devel/apr1 | apr-1.7.0.1.6.1_1
   [00:14:48] [02] [00:00:36] Finished security/libgpg-error | libgpg-error-1.41: Success
   [00:14:49] [02] [00:00:00] Building security/libassuan | libassuan-2.5.4
   [00:15:07] [02] [00:00:18] Finished security/libassuan | libassuan-2.5.4: Success
   [00:15:08] [02] [00:00:00] Building security/pinentry-curses | pinentry-curses-1.1.1
   [00:15:11] [03] [00:11:41] Finished lang/perl5.32 | perl5-5.32.1_1: Success
   [00:15:15] [03] [00:00:00] Building devel/p5-Locale-gettext | p5-Locale-gettext-1.07
   [00:15:15] [05] [00:00:00] Building textproc/p5-Unicode-EastAsianWidth | p5-Unicode-EastAsianWidth-12.0
   [00:15:15] [06] [00:00:00] Building converters/p5-Text-Unidecode | p5-Text-Unidecode-1.30
   [00:15:15] [07] [00:00:00] Building devel/p5-Locale-libintl | p5-Locale-libintl-1.32
   [00:15:15] [08] [00:00:00] Building security/ca_root_nss | ca_root_nss-3.63
   [00:15:15] [10] [00:00:00] Building converters/p5-Encode-Locale | p5-Encode-Locale-1.05
   [00:15:15] [09] [00:00:00] Building devel/p5-TimeDate | p5-TimeDate-2.33,1
   [00:15:15] [11] [00:00:00] Building security/libksba | libksba-1.5.0
   [00:15:15] [12] [00:00:00] Building devel/p5-Clone | p5-Clone-0.45
   [00:15:15] [13] [00:00:00] Building net/p5-URI | p5-URI-5.07
   [00:15:15] [14] [00:00:00] Building devel/p5-IO-HTML | p5-IO-HTML-1.001_1
   [00:15:15] [15] [00:00:00] Building www/p5-LWP-MediaTypes | p5-LWP-MediaTypes-6.04
   [00:15:15] [16] [00:00:00] Building textproc/utf8proc | utf8proc-2.6.1
   [00:15:35] [02] [00:00:27] Finished security/pinentry-curses | pinentry-curses-1.1.1: Success
   [00:15:36] [02] [00:00:00] Building security/pinentry | pinentry-1.1.1
   [00:15:44] [14] [00:00:29] Finished devel/p5-IO-HTML | p5-IO-HTML-1.001_1: Success
   [00:15:44] [10] [00:00:29] Finished converters/p5-Encode-Locale | p5-Encode-Locale-1.05: Success
   [00:15:44] [15] [00:00:29] Finished www/p5-LWP-MediaTypes | p5-LWP-MediaTypes-6.04: Success
   [00:15:44] [05] [00:00:29] Finished textproc/p5-Unicode-EastAsianWidth | p5-Unicode-EastAsianWidth-12.0: Success
   [00:15:45] [14] [00:00:00] Building www/p5-HTML-Tagset | p5-HTML-Tagset-3.20_1
   [00:15:45] [05] [00:00:00] Building net/p5-Socket6 | p5-Socket6-0.29
   [00:15:45] [10] [00:00:00] Building security/p5-Digest-HMAC | p5-Digest-HMAC-1.03_1
   [00:15:45] [15] [00:00:00] Building security/p5-GSSAPI | p5-GSSAPI-0.28_1
   [00:15:45] [16] [00:00:30] Finished textproc/utf8proc | utf8proc-2.6.1: Success
   [00:15:46] [09] [00:00:31] Finished devel/p5-TimeDate | p5-TimeDate-2.33,1: Success
   [00:15:46] [12] [00:00:31] Finished devel/p5-Clone | p5-Clone-0.45: Success
   [00:15:46] [16] [00:00:00] Building www/p5-Mozilla-CA | p5-Mozilla-CA-20200520
   [00:15:47] [02] [00:00:11] Finished security/pinentry | pinentry-1.1.1: Success
   [00:15:47] [03] [00:00:32] Finished devel/p5-Locale-gettext | p5-Locale-gettext-1.07: Success
   [00:15:47] [12] [00:00:00] Building www/p5-HTTP-Date | p5-HTTP-Date-6.05
   [00:15:47] [09] [00:00:00] Building security/p5-Net-SSLeay | p5-Net-SSLeay-1.88
   [00:15:47] [13] [00:00:32] Finished net/p5-URI | p5-URI-5.07: Success
   [00:15:49] [02] [00:00:00] Building lang/p5-Error | p5-Error-0.17029
   [00:15:49] [06] [00:00:34] Finished converters/p5-Text-Unidecode | p5-Text-Unidecode-1.30: Success
   [00:15:50] [03] [00:00:00] Building misc/help2man | help2man-1.48.1
   [00:15:50] [13] [00:00:00] Building devel/p5-Term-ReadKey | p5-Term-ReadKey-2.38_1
   [00:16:11] [07] [00:00:56] Finished devel/p5-Locale-libintl | p5-Locale-libintl-1.32: Success
   [00:16:13] [10] [00:00:28] Finished security/p5-Digest-HMAC | p5-Digest-HMAC-1.03_1: Success
   [00:16:13] [14] [00:00:28] Finished www/p5-HTML-Tagset | p5-HTML-Tagset-3.20_1: Success
   [00:16:13] [02] [00:00:24] Finished lang/p5-Error | p5-Error-0.17029: Success
   [00:16:17] [16] [00:00:31] Finished www/p5-Mozilla-CA | p5-Mozilla-CA-20200520: Success
   [00:16:18] [12] [00:00:31] Finished www/p5-HTTP-Date | p5-HTTP-Date-6.05: Success
   [00:16:18] [02] [00:00:00] Building www/p5-HTTP-Message | p5-HTTP-Message-6.28
   [00:16:19] [05] [00:00:34] Finished net/p5-Socket6 | p5-Socket6-0.29: Success
   [00:16:20] [15] [00:00:35] Finished security/p5-GSSAPI | p5-GSSAPI-0.28_1: Success
   [00:16:20] [05] [00:00:00] Building net/p5-IO-Socket-INET6 | p5-IO-Socket-INET6-2.72_1
   [00:16:20] [06] [00:00:00] Building security/p5-Authen-SASL | p5-Authen-SASL-2.16_1
   [00:16:22] [13] [00:00:32] Finished devel/p5-Term-ReadKey | p5-Term-ReadKey-2.38_1: Success
   [00:16:26] [03] [00:00:36] Finished misc/help2man | help2man-1.48.1: Success
   [00:16:26] [03] [00:00:00] Building print/texinfo | texinfo-6.7_4,1
   [00:16:36] [05] [00:00:16] Finished net/p5-IO-Socket-INET6 | p5-IO-Socket-INET6-2.72_1: Success
   [00:16:36] [02] [00:00:18] Finished www/p5-HTTP-Message | p5-HTTP-Message-6.28: Success
   [00:16:36] [05] [00:00:00] Building www/p5-HTML-Parser | p5-HTML-Parser-3.75
   [00:16:37] [06] [00:00:17] Finished security/p5-Authen-SASL | p5-Authen-SASL-2.16_1: Success
   [00:16:42] [11] [00:01:27] Finished security/libksba | libksba-1.5.0: Success
   [00:16:44] [09] [00:00:57] Finished security/p5-Net-SSLeay | p5-Net-SSLeay-1.88: Success
   [00:16:44] [02] [00:00:00] Building security/p5-IO-Socket-SSL | p5-IO-Socket-SSL-2.070
   [00:16:54] [05] [00:00:18] Finished www/p5-HTML-Parser | p5-HTML-Parser-3.75: Success
   [00:16:55] [05] [00:00:00] Building www/p5-CGI | p5-CGI-4.51
   [00:16:59] [02] [00:00:15] Finished security/p5-IO-Socket-SSL | p5-IO-Socket-SSL-2.070: Success
   [00:17:08] [05] [00:00:13] Finished www/p5-CGI | p5-CGI-4.51: Success
   [00:17:40] [08] [00:02:25] Finished security/ca_root_nss | ca_root_nss-3.63: Success
   [00:17:41] [02] [00:00:00] Building ftp/curl | curl-7.75.0
   [00:18:00] [04] [00:03:14] Finished devel/apr1 | apr-1.7.0.1.6.1_1: Success
   [00:18:11] [03] [00:01:45] Finished print/texinfo | texinfo-6.7_4,1: Success
   [00:18:12] [03] [00:00:00] Building devel/m4 | m4-1.4.18_1,1
   [00:18:12] [04] [00:00:00] Building security/libgcrypt | libgcrypt-1.9.2_1
   [00:18:12] [05] [00:00:00] Building math/gmp | gmp-6.2.1
   [00:18:12] [06] [00:00:00] Building ftp/wget | wget-1.21
   [00:19:22] [03] [00:01:10] Finished devel/m4 | m4-1.4.18_1,1: Success
   [00:19:22] [03] [00:00:00] Building devel/autoconf | autoconf-2.69_3
   [00:19:22] [07] [00:00:00] Building devel/libtool | libtool-2.4.6_1
   [00:19:22] [08] [00:00:00] Building devel/bison | bison-3.7.5,1
   [00:20:03] [07] [00:00:41] Finished devel/libtool | libtool-2.4.6_1: Success
   [00:20:07] [06] [00:01:55] Finished ftp/wget | wget-1.21: Success
   [00:20:09] [03] [00:00:47] Finished devel/autoconf | autoconf-2.69_3: Success
   [00:20:09] [03] [00:00:00] Building devel/automake | automake-1.16.3
   [00:20:32] [03] [00:00:23] Finished devel/automake | automake-1.16.3: Success
   [00:20:33] [03] [00:00:00] Building devel/libuv | libuv-1.41.0
   [00:20:33] [06] [00:00:00] Building devel/libatomic_ops | libatomic_ops-7.6.10
   [00:20:33] [07] [00:00:00] Building lang/ruby27 | ruby-2.7.2_1,1
   [00:20:33] [09] [00:00:00] Building devel/pcre2 | pcre2-10.36
   [00:20:46] [02] [00:03:05] Finished ftp/curl | curl-7.75.0: Success
   [00:20:54] [01] [00:06:42] Finished lang/python37 | python37-3.7.10: Success
   [00:20:57] [01] [00:00:00] Building devel/py-setuptools@py37 | py37-setuptools-44.0.0
   [00:20:57] [02] [00:00:00] Building devel/ninja | ninja-1.10.2,2
   [00:21:15] [06] [00:00:42] Finished devel/libatomic_ops | libatomic_ops-7.6.10: Success
   [00:21:15] [06] [00:00:00] Building devel/boehm-gc | boehm-gc-8.0.4_1
   [00:21:19] [01] [00:00:22] Finished devel/py-setuptools@py37 | py37-setuptools-44.0.0: Success
   [00:21:19] [01] [00:00:00] Building devel/py-pycparser@py37 | py37-pycparser-2.20
   [00:21:19] [10] [00:00:00] Building devel/py-six@py37 | py37-six-1.15.0
   [00:21:19] [11] [00:00:00] Building devel/py-pytz@py37 | py37-pytz-2020.5,1
   [00:21:19] [12] [00:00:00] Building net/py-pysocks@py37 | py37-pysocks-1.7.1
   [00:21:19] [13] [00:00:00] Building lang/cython@py37 | py37-cython-0.29.21
   [00:21:19] [14] [00:00:00] Building dns/py-idna@py37 | py37-idna-2.10
   [00:21:19] [15] [00:00:00] Building security/py-certifi@py37 | py37-certifi-2020.12.5
   [00:21:19] [16] [00:00:00] Building textproc/py-chardet@py37 | py37-chardet-3.0.4_3
   [00:21:24] [04] [00:03:12] Finished security/libgcrypt | libgcrypt-1.9.2_1: Success
   [00:21:25] [08] [00:02:03] Finished devel/bison | bison-3.7.5,1: Success
   [00:21:28] [04] [00:00:00] Building textproc/py-libxml2@py37 | py37-libxml2-2.9.10_3
   [00:21:29] [08] [00:00:00] Building textproc/py-markupsafe@py37 | py37-markupsafe-1.1.1_1
   [00:21:59] [10] [00:00:40] Finished devel/py-six@py37 | py37-six-1.15.0: Success
   [00:21:59] [12] [00:00:40] Finished net/py-pysocks@py37 | py37-pysocks-1.7.1: Success
   [00:21:59] [15] [00:00:40] Finished security/py-certifi@py37 | py37-certifi-2020.12.5: Success
   [00:21:59] [14] [00:00:40] Finished dns/py-idna@py37 | py37-idna-2.10: Success
   [00:22:00] [12] [00:00:00] Building devel/py-pyparsing@py37 | py37-pyparsing-2.4.7
   [00:22:00] [10] [00:00:00] Building textproc/py-sphinxcontrib-applehelp@py37 | py37-sphinxcontrib-applehelp-1.0.2
   [00:22:00] [15] [00:00:00] Building textproc/py-sphinxcontrib-devhelp@py37 | py37-sphinxcontrib-devhelp-1.0.2
   [00:22:00] [14] [00:00:00] Building textproc/py-docutils@py37 | py37-docutils-0.16
   [00:22:00] [16] [00:00:41] Finished textproc/py-chardet@py37 | py37-chardet-3.0.4_3: Success
   [00:22:02] [01] [00:00:43] Finished devel/py-pycparser@py37 | py37-pycparser-2.20: Success
   [00:22:03] [11] [00:00:44] Finished devel/py-pytz@py37 | py37-pytz-2020.5,1: Success
   [00:22:03] [16] [00:00:00] Building textproc/py-sphinxcontrib-htmlhelp@py37 | py37-sphinxcontrib-htmlhelp-1.0.3
   [00:22:04] [01] [00:00:00] Building devel/py-cffi@py37 | py37-cffi-1.14.5
   [00:22:05] [08] [00:00:36] Finished textproc/py-markupsafe@py37 | py37-markupsafe-1.1.1_1: Success
   [00:22:07] [11] [00:00:00] Building devel/py-babel@py37 | py37-Babel-2.9.0
   [00:22:07] [08] [00:00:00] Building graphics/py-imagesize@py37 | py37-imagesize-1.1.0
   [00:22:29] [06] [00:01:14] Finished devel/boehm-gc | boehm-gc-8.0.4_1: Success
   [00:22:31] [06] [00:00:01] Building textproc/py-sphinxcontrib-jsmath@py37 | py37-sphinxcontrib-jsmath-1.0.1
   [00:22:45] [15] [00:00:45] Finished textproc/py-sphinxcontrib-devhelp@py37 | py37-sphinxcontrib-devhelp-1.0.2: Success
   [00:22:45] [10] [00:00:45] Finished textproc/py-sphinxcontrib-applehelp@py37 | py37-sphinxcontrib-applehelp-1.0.2: Success
   [00:22:46] [12] [00:00:46] Finished devel/py-pyparsing@py37 | py37-pyparsing-2.4.7: Success
   [00:22:48] [15] [00:00:00] Building devel/py-packaging@py37 | py37-packaging-20.9
   [00:22:48] [12] [00:00:00] Building textproc/py-alabaster@py37 | py37-alabaster-0.7.6
   [00:22:48] [10] [00:00:00] Building textproc/py-sphinxcontrib-serializinghtml@py37 | py37-sphinxcontrib-serializinghtml-1.1.4
   [00:22:48] [04] [00:01:20] Finished textproc/py-libxml2@py37 | py37-libxml2-2.9.10_3: Success
   [00:22:54] [08] [00:00:47] Finished graphics/py-imagesize@py37 | py37-imagesize-1.1.0: Success
   [00:22:56] [04] [00:00:00] Building textproc/py-sphinxcontrib-qthelp@py37 | py37-sphinxcontrib-qthelp-1.0.3
   [00:22:56] [16] [00:00:53] Finished textproc/py-sphinxcontrib-htmlhelp@py37 | py37-sphinxcontrib-htmlhelp-1.0.3: Success
   [00:22:57] [03] [00:02:24] Finished devel/libuv | libuv-1.41.0: Success
   [00:22:58] [08] [00:00:00] Building textproc/libxslt | libxslt-1.1.34_1
   [00:22:59] [14] [00:00:59] Finished textproc/py-docutils@py37 | py37-docutils-0.16: Success
   [00:23:00] [03] [00:00:00] Building textproc/py-pygments@py37 | py37-pygments-2.7.2
   [00:23:00] [16] [00:00:00] Building textproc/itstool | itstool-2.0.6
   [00:23:03] [14] [00:00:00] Building shells/bash | bash-5.1.4_1
   [00:23:07] [06] [00:00:37] Finished textproc/py-sphinxcontrib-jsmath@py37 | py37-sphinxcontrib-jsmath-1.0.1: Success
   [00:23:08] [02] [00:02:11] Finished devel/ninja | ninja-1.10.2,2: Success
   [00:23:08] [01] [00:01:04] Finished devel/py-cffi@py37 | py37-cffi-1.14.5: Success
   [00:23:10] [06] [00:00:01] Building devel/scons@py37 | scons-py37-3.1.2
   [00:23:11] [02] [00:00:00] Building devel/meson | meson-0.57.1
   [00:23:12] [01] [00:00:00] Building security/py-cryptography@py37 | py37-cryptography-3.3.2
   [00:23:29] [12] [00:00:41] Finished textproc/py-alabaster@py37 | py37-alabaster-0.7.6: Success
   [00:23:29] [10] [00:00:41] Finished textproc/py-sphinxcontrib-serializinghtml@py37 | py37-sphinxcontrib-serializinghtml-1.1.4: Success
   [00:23:29] [15] [00:00:41] Finished devel/py-packaging@py37 | py37-packaging-20.9: Success
   [00:23:30] [12] [00:00:00] Building www/w3m | w3m-0.5.3.20210306
   [00:23:39] [11] [00:01:32] Finished devel/py-babel@py37 | py37-Babel-2.9.0: Success
   [00:23:40] [04] [00:00:44] Finished textproc/py-sphinxcontrib-qthelp@py37 | py37-sphinxcontrib-qthelp-1.0.3: Success
   [00:23:42] [15] [00:00:00] Building devel/py-Jinja2@py37 | py37-Jinja2-2.11.2_1
   [00:23:49] [16] [00:00:49] Finished textproc/itstool | itstool-2.0.6: Success
   [00:24:01] [03] [00:01:01] Finished textproc/py-pygments@py37 | py37-pygments-2.7.2: Success
   [00:24:07] [06] [00:00:58] Finished devel/scons@py37 | scons-py37-3.1.2: Success
   [00:24:07] [03] [00:00:00] Building www/serf | serf-1.3.9_6
   [00:24:12] [02] [00:01:01] Finished devel/meson | meson-0.57.1: Success
   [00:24:12] [15] [00:00:30] Finished devel/py-Jinja2@py37 | py37-Jinja2-2.11.2_1: Success
   [00:24:13] [02] [00:00:00] Building archivers/liblz4 | liblz4-1.9.3,1
   [00:24:13] [04] [00:00:00] Building devel/jsoncpp | jsoncpp-1.9.4
   [00:24:28] [05] [00:06:16] Finished math/gmp | gmp-6.2.1: Success
   [00:24:30] [05] [00:00:00] Building security/nettle | nettle-3.6
   [00:24:43] [01] [00:01:31] Finished security/py-cryptography@py37 | py37-cryptography-3.3.2: Success
   [00:24:44] [01] [00:00:00] Building security/py-openssl@py37 | py37-openssl-20.0.1
   [00:24:45] [08] [00:01:47] Finished textproc/libxslt | libxslt-1.1.34_1: Success
   [00:24:46] [06] [00:00:00] Building textproc/yelp-xsl | yelp-xsl-3.38.3
   [00:24:46] [08] [00:00:00] Building devel/glib20 | glib-2.66.7_1,1
   [00:24:55] [03] [00:00:48] Finished www/serf | serf-1.3.9_6: Success
   [00:25:03] [02] [00:00:50] Finished archivers/liblz4 | liblz4-1.9.3,1: Success
   [00:25:03] [02] [00:00:00] Building archivers/libarchive | libarchive-3.5.1,1
   [00:25:03] [03] [00:00:00] Building archivers/zstd | zstd-1.4.8
   [00:25:07] [01] [00:00:23] Finished security/py-openssl@py37 | py37-openssl-20.0.1: Success
   [00:25:08] [01] [00:00:00] Building net/py-urllib3@py37 | py37-urllib3-1.25.11,1
   [00:25:15] [13] [00:03:56] Finished lang/cython@py37 | py37-cython-0.29.21: Success
   [00:25:17] [10] [00:00:00] Building textproc/py-pystemmer@py37 | py37-pystemmer-2.0.0.1
   [00:25:18] [06] [00:00:32] Finished textproc/yelp-xsl | yelp-xsl-3.38.3: Success
   [00:25:19] [06] [00:00:00] Building textproc/yelp-tools | yelp-tools-3.38.0
   [00:25:28] [12] [00:01:58] Finished www/w3m | w3m-0.5.3.20210306: Success
   [00:25:37] [01] [00:00:29] Finished net/py-urllib3@py37 | py37-urllib3-1.25.11,1: Success
   [00:25:38] [01] [00:00:00] Building www/py-requests@py37 | py37-requests-2.22.0_2
   [00:25:44] [04] [00:01:31] Finished devel/jsoncpp | jsoncpp-1.9.4: Success
   [00:25:45] [06] [00:00:26] Finished textproc/yelp-tools | yelp-tools-3.38.0: Success
   [00:25:45] [04] [00:00:00] Building textproc/gtk-doc | gtk-doc-1.33.2
   [00:25:55] [10] [00:00:38] Finished textproc/py-pystemmer@py37 | py37-pystemmer-2.0.0.1: Success
   [00:25:55] [06] [00:00:00] Building textproc/py-snowballstemmer@py37 | py37-snowballstemmer-1.2.1
   [00:26:00] [01] [00:00:22] Finished www/py-requests@py37 | py37-requests-2.22.0_2: Success
   [00:26:14] [06] [00:00:19] Finished textproc/py-snowballstemmer@py37 | py37-snowballstemmer-1.2.1: Success
   [00:26:15] [01] [00:00:00] Building textproc/py-sphinx@py37 | py37-sphinx-3.5.2,1
   [00:26:19] [14] [00:03:16] Finished shells/bash | bash-5.1.4_1: Success
   [00:26:19] [06] [00:00:00] Building shells/bash-completion | bash-completion-2.11,2
   [00:26:19] [10] [00:00:00] Building textproc/xmlto | xmlto-0.0.28
   [00:26:49] [10] [00:00:30] Finished textproc/xmlto | xmlto-0.0.28: Success
   [00:26:50] [04] [00:01:05] Finished textproc/gtk-doc | gtk-doc-1.33.2: Success
   [00:26:51] [06] [00:00:32] Finished shells/bash-completion | bash-completion-2.11,2: Success
   [00:26:56] [05] [00:02:26] Finished security/nettle | nettle-3.6: Success
   [00:27:03] [01] [00:00:48] Finished textproc/py-sphinx@py37 | py37-sphinx-3.5.2,1: Success
   [00:27:04] [03] [00:02:01] Finished archivers/zstd | zstd-1.4.8: Success
   [00:27:05] [01] [00:00:00] Building net/rsync | rsync-3.2.3
   [00:27:38] [09] [00:07:05] Finished devel/pcre2 | pcre2-10.36: Success
   [00:27:49] [01] [00:00:44] Finished net/rsync | rsync-3.2.3: Success
   [00:28:02] [02] [00:02:59] Finished archivers/libarchive | libarchive-3.5.1,1: Success
   [00:28:03] [01] [00:00:00] Building devel/cmake | cmake-3.19.6
   [00:33:40] [08] [00:08:54] Finished devel/glib20 | glib-2.66.7_1,1: Success
   [00:33:41] [02] [00:00:00] Building security/p11-kit | p11-kit-0.23.22_1
   [00:34:56] [02] [00:01:15] Finished security/p11-kit | p11-kit-0.23.22_1: Success
   [00:35:51] [07] [00:15:18] Finished lang/ruby27 | ruby-2.7.2_1,1: Success
   [00:35:59] [02] [00:00:00] Building devel/ruby-gems | ruby27-gems-3.0.8
   [00:36:24] [02] [00:00:25] Finished devel/ruby-gems | ruby27-gems-3.0.8: Success
   [00:36:24] [02] [00:00:00] Building devel/rubygem-rdoc | rubygem-rdoc-6.3.0
   [00:36:24] [03] [00:00:00] Building textproc/rubygem-asciidoctor | rubygem-asciidoctor-2.0.12
   [00:36:45] [03] [00:00:21] Finished textproc/rubygem-asciidoctor | rubygem-asciidoctor-2.0.12: Success
   [00:36:48] [02] [00:00:24] Finished devel/rubygem-rdoc | rubygem-rdoc-6.3.0: Success
   [00:36:48] [02] [00:00:00] Building databases/ruby-bdb | ruby27-bdb-0.6.6_8
   [00:39:20] [02] [00:02:32] Finished databases/ruby-bdb | ruby27-bdb-0.6.6_8: Failed: stage
   [00:39:20] [02] [00:02:32] Skipping ports-mgmt/portupgrade | portupgrade-2.4.16,2: Dependent port databases/ruby-bdb | ruby27-bdb-0.6.6_8 failed
   [01:13:09] [01] [00:45:06] Finished devel/cmake | cmake-3.19.6: Success
   [01:13:13] [01] [00:00:00] Building emulators/tpm-emulator | tpm-emulator-0.7.4_2
   [01:13:50] [01] [00:00:37] Finished emulators/tpm-emulator | tpm-emulator-0.7.4_2: Success
   [01:13:50] [01] [00:00:00] Building security/trousers | trousers-0.3.14_3
   [01:18:40] [01] [00:04:50] Finished security/trousers | trousers-0.3.14_3: Success
   [01:18:40] [01] [00:00:00] Building security/gnutls | gnutls-3.6.15
   [01:25:14] [01] [00:06:34] Finished security/gnutls | gnutls-3.6.15: Success
   [01:25:16] [01] [00:00:00] Building security/gnupg | gnupg-2.2.27
   [01:28:53] [01] [00:03:37] Finished security/gnupg | gnupg-2.2.27: Success
   [01:28:53] [01] [00:00:00] Building devel/subversion | subversion-1.14.1
   [01:39:25] [01] [00:10:32] Finished devel/subversion | subversion-1.14.1: Success
   [01:39:27] [01] [00:00:00] Building devel/p5-subversion | p5-subversion-1.14.1
   [01:42:51] [01] [00:03:24] Finished devel/p5-subversion | p5-subversion-1.14.1: Success
   [01:42:51] [01] [00:00:00] Building devel/git@default | git-2.31.0
   [01:51:01] [01] [00:08:10] Finished devel/git@default | git-2.31.0: Success
   [01:51:02] Stopping 16 builders
   [01:52:27] Creating pkg repository
   Creating repository in /tmp/packages: 100%
   Packing files for repository: 100%
   [01:52:29] Committing packages to repository: /zroot/poudriere/data/packages/12amd64-local-devel/.real_1616456087 via .latest symlink
   [01:52:29] Removing old packages
   [01:52:30] Built ports: ports-mgmt/pkg devel/autoconf-wrapper print/indexinfo ports-mgmt/portmaster devel/cvsps textproc/xmlcatmgr print/libpaper devel/npth textproc/xmlcharent textproc/iso8879 textproc/sdocbook-xml textproc/docbook-sgml textproc/docbook-xml devel/libffi devel/pkgconf textproc/docbook textproc/expat2 devel/libedit devel/readline converters/libiconv security/libtasn1 www/libnghttp2 devel/gettext-runtime textproc/docbook-xsl devel/libunwind devel/gmake devel/xxhash devel/libltdl textproc/libyaml devel/libtextstyle archivers/gtar lang/tcl86 textproc/libxml2 devel/libunistring dns/libidn2 devel/pcre databases/db5 databases/sqlite3 devel/gettext-tools misc/getopt security/rhash databases/gdbm security/libgpg-error security/libassuan lang/perl5.32 security/pinentry-curses devel/p5-IO-HTML converters/p5-Encode-Locale www/p5-LWP-MediaTypes textproc/p5-Unicode-EastAsianWidth textproc/utf8proc devel/p5-TimeDate devel/p5-Clone security/pinentry devel/p5-Locale-gettext net/p5-URI converters/p5-Text-Unidecode devel/p5-Locale-libintl security/p5-Digest-HMAC www/p5-HTML-Tagset lang/p5-Error www/p5-Mozilla-CA www/p5-HTTP-Date net/p5-Socket6 security/p5-GSSAPI devel/p5-Term-ReadKey misc/help2man net/p5-IO-Socket-INET6 www/p5-HTTP-Message security/p5-Authen-SASL security/libksba security/p5-Net-SSLeay www/p5-HTML-Parser security/p5-IO-Socket-SSL www/p5-CGI security/ca_root_nss devel/apr1 print/texinfo devel/m4 devel/libtool ftp/wget devel/autoconf devel/automake ftp/curl lang/python37 devel/libatomic_ops devel/py-setuptools security/libgcrypt devel/bison devel/py-six net/py-pysocks security/py-certifi dns/py-idna textproc/py-chardet devel/py-pycparser devel/py-pytz textproc/py-markupsafe devel/boehm-gc textproc/py-sphinxcontrib-devhelp textproc/py-sphinxcontrib-applehelp devel/py-pyparsing textproc/py-libxml2 graphics/py-imagesize textproc/py-sphinxcontrib-htmlhelp devel/libuv textproc/py-docutils textproc/py-sphinxcontrib-jsmath devel/ninja devel/py-cffi textproc/py-alabaster textproc/py-sphinxcontrib-serializinghtml devel/py-packaging devel/py-babel textproc/py-sphinxcontrib-qthelp textproc/itstool textproc/py-pygments devel/scons devel/meson devel/py-Jinja2 math/gmp security/py-cryptography textproc/libxslt www/serf archivers/liblz4 security/py-openssl lang/cython textproc/yelp-xsl www/w3m net/py-urllib3 devel/jsoncpp textproc/yelp-tools textproc/py-pystemmer www/py-requests textproc/py-snowballstemmer shells/bash textproc/xmlto textproc/gtk-doc shells/bash-completion security/nettle textproc/py-sphinx archivers/zstd devel/pcre2 net/rsync archivers/libarchive devel/glib20 security/p11-kit lang/ruby27 devel/ruby-gems textproc/rubygem-asciidoctor devel/rubygem-rdoc devel/cmake emulators/tpm-emulator security/trousers security/gnutls security/gnupg devel/subversion devel/p5-subversion devel/git
   [01:52:30] Failed ports: databases/ruby-bdb:stage
   [01:52:30] Skipped ports: ports-mgmt/portupgrade
   [12amd64-local-devel] [2021-03-22_22h42m18s] [committing:] Queued: 160 Built: 158 Failed: 1   Skipped: 1   Ignored: 0   Tobuild: 0    Time: 01:52:20
   [01:52:30] Logs: /zroot/poudriere/data/logs/bulk/12amd64-local-devel/2021-03-22_22h42m18s
   [01:52:30] WWW: http://build.example.com//build.html?mastername=12amd64-local-devel&build=2021-03-22_22h42m18s
   [01:52:30] Cleaning up
   [01:52:30] Unmounting file systems

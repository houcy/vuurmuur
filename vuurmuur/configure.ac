AC_INIT([vuurmuur],[0.8rc2])
AC_CONFIG_SRCDIR([vuurmuur/vuurmuur.c])
AM_INIT_AUTOMAKE

AM_CONFIG_HEADER(config.h)
AC_CONFIG_MACRO_DIR([m4])

AC_LANG_C
AC_PROG_CC
AM_PROG_LIBTOOL

AC_ARG_WITH(libvuurmuur_includes,
	[  --with-libvuurmuur-includes=DIR  libvuurmuur includes directory],
	[with_libvuurmuur_includes="$withval"],[with_libvuurmuur_includes=no])

AC_ARG_WITH(libvuurmuur_libraries,
       [  --with-libvuurmuur-libraries=DIR  libvuurmuur library directory],
       [with_libvuurmuur_libraries="$withval"],[with_libvuurmuur_libraries=no])

if test "$with_libvuurmuur_includes" != "no"; then
   CPPFLAGS="${CPPFLAGS} -I${with_libvuurmuur_includes}"
fi

if test "$with_libvuurmuur_libraries" != "no"; then
   LDFLAGS="${LDFLAGS}  -L${with_libvuurmuur_libraries}"
fi

ac_build_ipv6=yes
AC_ARG_ENABLE([ipv6],
        [AS_HELP_STRING([--disable-ipv6],[disable IPv6 support])],
        [ if test "x$enableval" = "xno"; then
            ac_build_ipv6=$enableval
          fi
        ], [
            ac_build_ipv6=yes
        ] )

if test "x${ac_build_ipv6}" = "xyes"; then
    AC_DEFINE(IPV6_ENABLED, 1, [build with IPv6 support])
fi

LVUUR=""
AC_CHECK_HEADERS(vuurmuur.h,, LVUUR="no")
if test "$LVUUR" = "no"; then
	echo
	echo "   ERROR!  vuurmuur.h header not found, go get it from"
	echo "   http://www.vuurmuur.org/"
	exit
fi

LVUUR=""
AC_CHECK_LIB(vuurmuur,libvuurmuur_get_version,, LVUUR="no")
if test "$LVUUR" = "no"; then
	echo
	echo "   ERROR!  libvuurmuur library not found, go get it from"
	echo "   http://www.vuurmuur.org/"
	exit
fi

# nfnetlink lib
AC_ARG_WITH(libnfnetlink_includes,
        [  --with-libnfnetlink-includes=DIR  libnfnetlink include directory],
        [with_libnfnetlink_includes="$withval"],[with_libnfnetlink_includes=no])
AC_ARG_WITH(libnfnetlink_libraries,
        [  --with-libnfnetlink-libraries=DIR    libnfnetlink library directory],
        [with_libnfnetlink_libraries="$withval"],[with_libnfnetlink_libraries="no"])

if test "$with_libnfnetlink_includes" != "no"; then
CPPFLAGS="${CPPFLAGS} -I${with_libnfnetlink_includes}"
fi
AC_CHECK_HEADER(libnfnetlink/libnfnetlink.h,,)

if test "$with_libnfnetlink_libraries" != "no"; then
LDFLAGS="${LDFLAGS}  -L${with_libnfnetlink_libraries}"
fi

AC_CHECK_LIB(nfnetlink, nfnl_fd,, NFNETLINK="no")
if test "$NFNETLINK" != "no"; then
CFLAGS="${CFLAGS} -DHAVE_NFNETLINK"
fi

# netfilter_conntrack lib
AC_ARG_WITH(libnetfilter_conntrack_includes,
        [  --with-libnetfilter_conntrack-includes=DIR  libnetfilter_conntrack include directory],
        [with_libnetfilter_conntrack_includes="$withval"],[with_libnetfilter_conntrack_includes=no])
AC_ARG_WITH(libnetfilter_conntrack_libraries,
        [  --with-libnetfilter_conntrack-libraries=DIR    libnetfilter_conntrack library directory],
        [with_libnetfilter_conntrack_libraries="$withval"],[with_libnetfilter_conntrack_libraries="no"])

if test "$with_libnetfilter_conntrack_includes" != "no"; then
CPPFLAGS="${CPPFLAGS} -I${with_libnetfilter_conntrack_includes}"
fi
AC_CHECK_HEADER(libnetfilter_conntrack/libnetfilter_conntrack.h,,)

if test "$with_libnetfilter_conntrack_libraries" != "no"; then
LDFLAGS="${LDFLAGS}  -L${with_libnetfilter_conntrack_libraries}"
fi

AC_CHECK_LIB(netfilter_conntrack, nfct_fd,, NFCONNTRACK="no")
if test "$NFCONNTRACK" != "no"; then
CFLAGS="${CFLAGS} -DHAVE_LIBNETFILTER_CONNTRACK"
fi

# netfilter_log lib
AC_ARG_WITH(libnetfilter_log_includes,
        [  --with-libnetfilter_log-includes=DIR  libnetfilter_log include directory],
        [with_libnetfilter_log_includes="$withval"],[with_libnetfilter_log_includes=no])
AC_ARG_WITH(libnetfilter_log_libraries,
        [  --with-libnetfilter_log-libraries=DIR    libnetfilter_log library directory],
        [with_libnetfilter_log_libraries="$withval"],[with_libnetfilter_log_libraries="no"])

if test "$with_libnetfilter_log_includes" != "no"; then
CPPFLAGS="${CPPFLAGS} -I${with_libnetfilter_log_includes}"
fi
AC_CHECK_HEADER(libnetfilter_log/libnetfilter_log.h,,)

if test "$with_libnetfilter_log_libraries" != "no"; then
LDFLAGS="${LDFLAGS}  -L${with_libnetfilter_log_libraries}"
fi

AC_CHECK_LIB(netfilter_log, nflog_open,, NFLOG="no")
if test "$NFLOG" != "no"; then
CFLAGS="${CFLAGS} -DHAVE_LIBNETFILTER_LOG"
fi

AC_OUTPUT(Makefile vuurmuur/Makefile vuurmuur_log/Makefile
	    vuurmuur_script/Makefile scripts/Makefile services/Makefile
	    config/Makefile man/Makefile man/en/Makefile man/ru/Makefile
        debian/Makefile)


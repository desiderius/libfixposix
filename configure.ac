dnl Process this file with autoconf to produce a configure script.
dnl
dnl This file is free software; as a special exception the author gives
dnl unlimited permission to copy and/or distribute it, with or without
dnl modifications, as long as this notice is preserved.
dnl
dnl This program is distributed in the hope that it will be useful, but
dnl WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
dnl implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

dnl Minimum Autoconf version required.
AC_PREREQ([2.67])

AC_INIT([LibFixPOSIX], [0.3.0], [iolib-devel@common-lisp.net],
        [libfixposix], [http://common-lisp.net/project/iolib/])
AC_COPYRIGHT([Copyright © 2010-2014 Stelian Ionescu <sionescu@cddr.org>])

AC_MSG_NOTICE([srcdir:   $srcdir])
AC_MSG_NOTICE([builddir: $builddir])
AC_MSG_NOTICE([CPPFLAGS: $CPPFLAGS])
AC_MSG_NOTICE([CFLAGS:   $CFLAGS])
AC_MSG_NOTICE([LDFLAGS:  $LDFLAGS])
AS_IF([test "`/bin/pwd`" = "`cd $srcdir; /bin/pwd`"], [
  AC_MSG_WARN([you should configure in a separate build directory])
])

AC_CONFIG_HEADERS([config.h])

dnl Where to generate output; srcdir location.
AC_CONFIG_SRCDIR([src/lib/spawn.c])

dnl Auxiliary M4 macros
AC_CONFIG_MACRO_DIR([config/m4])

dnl Must come before AM_INIT_AUTOMAKE.
AC_CONFIG_AUX_DIR([config/aux])

AM_INIT_AUTOMAKE([1.10 foreign silent-rules subdir-objects
                  color-tests parallel-tests])

dnl Have Kbuild-like build output
AM_SILENT_RULES([yes])

dnl Contains replacement functions
# AC_CONFIG_LIBOBJ_DIR([lib])

AC_LANG([C])

dnl Checks for programs.
# We need a C compiler.
AC_PROG_CC_C99
AC_PROG_AWK
# And we need libtool for building the shared library
LT_INIT([pic-only disable-static disable-fast-install])
LT_PREREQ([2.2.6])

LFP_INIT

dnl Checks for programs
LFP_REQUIRE_PROG([GETCONF], [getconf])

dnl Set compiler & linker flags
LFP_SYS_PLATFORM_SPECIFIC_DEFINITIONS
AX_PTHREAD
LFP_SYS_LARGEFILE

dnl Checks for C99 & POSIX headers
AC_HEADER_ASSERT
AC_HEADER_STDBOOL
LFP_REQUIRE_HEADERS([stdlib.h stdio.h string.h errno.h time.h])
LFP_REQUIRE_HEADERS([sys/types.h unistd.h fcntl.h sys/signal.h signal.h])

LFP_CFLAGS="$LFP_CFLAGS $LFS_CFLAGS $PTHREAD_CFLAGS"
LFP_LDFLAGS="$LFP_LDFLAGS $LFS_LDFLAGS"
LFP_LIBS="$LFP_LIBS $PTHREAD_LIBS $LFS_LIBS"

dnl Checks for declarations
LFP_REQUIRE_DECL([TIOCSCTTY], [sys/ioctl.h])
LFP_REQUIRE_DECL([NSIG], [sys/types.h sys/signal.h signal.h])
LFP_REQUIRE_DECL([IP_HDRINCL], [sys/types.h sys/socket.h netinet/in.h])

dnl Checks for non-standard headers
AC_CHECK_HEADER([sys/signalfd.h])

dnl Checks for functions
AC_CHECK_FUNCS([__xpg_strerror_r strnlen strndup clearenv])
LFP_REQUIRE_FUNCS([strtok_r])
LFP_SEARCH_LIBS([socket], [socket nsl])
AC_CHECK_FUNCS([accept4 pipe2 sendfile pselect ptsname_r])
LFP_REQUIRE_FUNCS([vsyslog ptsname posix_openpt])
LFP_REQUIRE_MONOTONIC_CLOCK
LFP_REQUIRE_GETPEEREID

dnl Checks for types

dnl Configuration switches
# LFP_ARG_ENABLE_EMULATED_SIGNALFD

LFP_TESTS_CHECK

AC_CONFIG_FILES([Makefile
                 src/libfixposix.pc
                 src/include/lfp/time.h])
AC_OUTPUT

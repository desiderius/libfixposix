# -*- makefile-automake -*-

########################################################################
#                                                                      #
#                        Global Automake variables                     #
#                                                                      #
########################################################################

ACLOCAL_AMFLAGS = -I config/m4

AM_CFLAGS = $(LFP_CFLAGS) -fvisibility=hidden

AM_CPPFLAGS = -include $(top_builddir)/config.h \
	      -include $(top_srcdir)/src/lib/aux/macros.h \
	      -I$(top_srcdir)/src/include \
	      -I$(top_builddir)/src/include

EXTRA_DIST = \
	LICENCE \
	src/libfixposix.libtool



########################################################################
#                                                                      #
#                              PKG-CONFIG                              #
#                                                                      #
########################################################################

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = src/libfixposix.pc



########################################################################
#                                                                      #
#                             libfixposix.so                           #
#                                                                      #
########################################################################

lib_LTLIBRARIES = src/lib/libfixposix.la

# Private headers, used only for internal definitions
# The only purpose of this definition it to ensure that
#  «make dist» knows about them
noinst_HEADERS = \
	src/lib/aux/inlines.h \
	src/lib/aux/macros.h \
	src/lib/spawn.h

include_HEADERS = src/include/lfp.h

include_lfpdir = $(includedir)/lfp
include_lfp_HEADERS = \
	src/include/lfp/aux.h \
	src/include/lfp/stdlib.h \
	src/include/lfp/string.h \
	src/include/lfp/strerror.h \
	src/include/lfp/errno.h \
	src/include/lfp/fcntl.h \
	src/include/lfp/stat.h \
	src/include/lfp/unistd.h \
	src/include/lfp/ioctl.h \
	src/include/lfp/mman.h \
	src/include/lfp/select.h \
	src/include/lfp/socket.h \
	src/include/lfp/wait.h \
	src/include/lfp/signal.h \
	src/include/lfp/spawn.h \
	src/include/lfp/dirent.h \
	$(top_builddir)/src/include/lfp/time.h \
	src/include/lfp/resource.h \
	src/include/lfp/sendfile.h \
	src/include/lfp/syslog.h
# src/include/lfp/signalfd.h

src_lib_libfixposix_la_SOURCES = \
	src/lib/stdlib.c \
	src/lib/string.c \
	src/lib/strerror.c \
	src/lib/errno.c \
	src/lib/fcntl.c \
	src/lib/stat.c \
	src/lib/unistd.c \
	src/lib/ioctl.c \
	src/lib/mman.c \
	src/lib/select.c \
	src/lib/socket.c \
	src/lib/wait.c \
	src/lib/signal.c \
	src/lib/spawnattr.c \
	src/lib/bitset.c \
	src/lib/spawn_file_actions.c \
	src/lib/spawn.c \
	src/lib/dirent.c \
	src/lib/time.c \
	src/lib/resource.c \
	src/lib/sendfile.c \
	src/lib/syslog.c
# src/lib/install_signalfd.c

src_lib_libfixposix_la_DEPENDENCIES = \
	src/libfixposix.libtool

src_lib_libfixposix_la_LIBADD = $(LFP_LIBS)

src_lib_libfixposix_la_LDFLAGS = $(LFP_LDFLAGS) -no-undefined \
	-version-info `@AWK@ '/^Version:/ { print $$2 }' $(top_srcdir)/src/libfixposix.libtool`



########################################################################
#                                                                      #
#                                TESTS                                 #
#                                                             	       #
########################################################################


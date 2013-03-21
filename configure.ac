#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([mod_hfs_apple], [11])
AC_CONFIG_SRCDIR([mod_hfs_apple2.c])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])
AM_INIT_AUTOMAKE([foreign])
AM_MAINTAINER_MODE
AC_CANONICAL_HOST

# Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PATH_PROG([APXS], [apxs])
AC_SUBST(APXS)
AX_PROG_APACHE
AX_PROG_HTTPD
AX_CHECK_GNU_MAKE
AC_PROG_LIBTOOL

# Checks for libraries.

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([ctype.h unistd.h])
AC_CHECK_HEADERS([CoreServices/../Frameworks/CarbonCore.framework/Headers/MacErrors.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_TYPE_SIZE_T

# Checks for library functions.
AC_FUNC_MALLOC
AC_CHECK_FUNCS([pathconf])

AC_CONFIG_FILES([Makefile Makefile.orig])
AC_OUTPUT

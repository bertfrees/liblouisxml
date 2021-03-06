# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
AC_INIT(liblouisxml, 2.4.0, john.boyer@abilitiessoft.com)
AC_CONFIG_SRCDIR([liblouisxml/semantics.c])
AC_CONFIG_HEADER([liblouisxml/config.h])
# AM_MAINTAINER_MODE

AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE(AC_PACKAGE_NAME, AC_PACKAGE_VERSION)

# increment if the interface has additions, changes, removals.
LIBLOUISXML_CURRENT=3

# increment any time the source changes; set to
#  0 if you increment CURRENT
LIBLOUISXML_REVISION=0

# increment if any interfaces have been added; set to 0
#  if any interfaces have been changed or removed. removal has
#  precedence over adding, so set to 0 if both happened.
LIBLOUISXML_AGE=2

AC_SUBST(LIBLOUISXML_CURRENT)
AC_SUBST(LIBLOUISXML_REVISION)
AC_SUBST(LIBLOUISXML_AGE)

# Checks for programs.
AC_PROG_CC

# gnulib
gl_EARLY
gl_INIT

# make sure we have a decent malloc and realloc
gl_FUNC_MALLOC_GNU
if test $REPLACE_MALLOC = 1; then
AC_LIBOBJ([malloc])
fi
gl_MODULE_INDICATOR([malloc-gnu])

gl_FUNC_REALLOC_GNU
if test $REPLACE_REALLOC = 1; then
AC_LIBOBJ([realloc])
fi
gl_MODULE_INDICATOR([realloc-gnu])

# Checks for more programs.
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
# AC_PROG_RANLIB
AC_ISC_POSIX
AC_LIBTOOL_WIN32_DLL
AM_PROG_LIBTOOL

# GNU help2man creates man pages from --help output; in many cases,
# this is sufficient, and obviates the need to maintain man pages
# separately. However, some developers do not have it so we do not
# make its use mandatory.
AC_CHECK_PROG([HELP2MAN], [help2man], [help2man])
AM_CONDITIONAL([HAVE_HELP2MAN], [test x$HELP2MAN = xhelp2man])

AC_PATH_PROG(PKG_CONFIG, pkg-config)

PKG_CHECK_MODULES(BASE_DEPENDENCIES, [liblouis, libxml-2.0])

# Checks for libraries.

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([stdlib.h string.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST

# Checks for library functions.
AC_FUNC_STAT
AC_CHECK_FUNCS([memset])

case $host in
  *mingw* | *cygwin*)
    LDFLAGS="$LDFLAGS -avoid-version"
    CFLAGS="$CFLAGS -Wl,--add-stdcall-alias"
  ;;
esac

AC_CONFIG_FILES([Makefile
		 gnulib/Makefile
                 doc/Makefile
		 man/Makefile
                 lbx_files/Makefile
                 liblouisxml/Makefile
                 tests/Makefile
		 liblouisxml.pc
                 tools/Makefile
                 python/Makefile
		 m4/Makefile])

AC_CONFIG_FILES([tools/msword2brl], [chmod +x tools/msword2brl])
AC_CONFIG_FILES([tools/rtf2brl], [chmod +x tools/rtf2brl])
AC_CONFIG_FILES([tools/pdf2brl], [chmod +x tools/pdf2brl])

AC_OUTPUT


AC_PREREQ(2.59)
AC_INIT(tang, 6)
AC_CANONICAL_SYSTEM
AC_PROG_CC_C99
AC_PROG_SED

AM_INIT_AUTOMAKE([subdir-objects foreign no-dist-gzip dist-bzip2 parallel-tests])
AM_SILENT_RULES([yes])
AM_PROG_CC_C_O

PKG_PROG_PKG_CONFIG([0.25])

AC_CHECK_LIB([dl], [dlopen], [AC_SUBST([dl_LIBS], [-ldl])],
             [AC_CHECK_LIB([dl], [dlopen], [AC_SUBST([dl_LIBS], [-ldl])],
	                   [AC_MSG_ERROR([unable to find dlopen])])])

AC_CHECK_HEADER([http_parser.h], [],
		[AC_MSG_ERROR([http-parser required!])], [
#include <http_parser.h>
#ifndef HTTP_STATUS_MAP
#error HTTP_STATUS_MAP not defined!
#endif
])

AC_CHECK_LIB([http_parser], [http_parser_execute],
             [AC_SUBST(http_parser_LIBS, [-lhttp_parser])],
             [AC_MSG_ERROR([http-parser required!])])

PKG_CHECK_MODULES([jose], [jose >= 8])

#PKG_CHECK([xinetd], [xinetd])

TANG_CFLAGS="\
-Wall \
-Wextra \
-Werror \
-Wstrict-aliasing \
-Wchar-subscripts \
-Wformat-security \
-Wmissing-declarations \
-Wmissing-prototypes \
-Wnested-externs \
-Wpointer-arith \
-Wshadow \
-Wsign-compare \
-Wstrict-prototypes \
-Wtype-limits \
-Wunused-function \
-Wno-missing-field-initializers \
-Wno-unused-parameter \
"
AC_SUBST([TANG_CFLAGS])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT

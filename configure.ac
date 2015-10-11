AC_PREREQ([2.69])

AC_INIT([blogc-runserver], [0.1], [https://github.com/blogc/blogc-runserver])
AC_CONFIG_AUX_DIR([build-aux])

AM_INIT_AUTOMAKE([1.13 foreign dist-bzip2 dist-xz subdir-objects serial-tests])
AC_CONFIG_HEADERS([config.h])
AM_SILENT_RULES([yes])
AM_MAINTAINER_MODE([enable])

AC_USE_SYSTEM_EXTENSIONS

AC_PROG_CC_C99
AS_IF([test "x$ac_cv_prog_cc_c99" = "xno"], [
  AC_MSG_ERROR([no C99 compiler found, blogc-runserver requires a C99 compiler.])
])

AC_CHECK_HEADERS([signal.h stdarg.h fcntl.h unistd.h sys/stat.h sys/types.h], [],
  [unable to find some required header])

AC_CHECK_HEADERS([magic.h], [], [unable to find libmagic headers])

AC_CHECK_LIB(magic, [magic_open], [MAGIC_LIBS="-lmagic"], [
  AC_MSG_ERROR([unable to find libmagic])
])
AC_SUBST(MAGIC_LIBS)

PKG_PROG_PKG_CONFIG
PKG_CHECK_MODULES([LIBEVENT], [libevent >= 2.0])

AC_CONFIG_FILES([Makefile])
AC_OUTPUT

AS_ECHO("
        ==== ${PACKAGE_STRING} ====

        prefix:       ${prefix}
        exec_prefix:  ${exec_prefix}
        bindir:       ${bindir}

        compiler:     ${CC}
        cflags:       ${CFLAGS}
        ldflags:      ${LDFLAGS}
")

AC_PREREQ([2.69])

AC_INIT([blogc-runserver], m4_esyscmd([build-aux/git-version-gen .tarball-version]),
        [https://github.com/blogc/blogc-runserver], [blogc-runserver],
        [https://blogc.rgm.io/])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])

AM_INIT_AUTOMAKE([1.13 foreign dist-bzip2 dist-xz subdir-objects serial-tests])
AC_CONFIG_HEADERS([config.h])
AM_SILENT_RULES([yes])
AM_MAINTAINER_MODE([enable])

AC_USE_SYSTEM_EXTENSIONS

LT_INIT

AC_PROG_CC_C99
AS_IF([test "x$ac_cv_prog_cc_c99" = "xno"], [
  AC_MSG_ERROR([no C99 compiler found, blogc-runserver requires a C99 compiler.])
])

AC_CHECK_HEADERS([signal.h stdarg.h fcntl.h unistd.h sys/stat.h sys/types.h], , [
  AC_MSG_ERROR([unable to find some required header])
])

AC_CHECK_HEADERS([magic.h], , [
  AC_MSG_ERROR([unable to find libmagic headers])
])

AC_CHECK_LIB(magic, [magic_open], [MAGIC_LIBS="-lmagic"], [
  AC_MSG_ERROR([unable to find libmagic])
])
AC_SUBST(MAGIC_LIBS)

PKG_PROG_PKG_CONFIG
PKG_CHECK_MODULES([LIBEVENT], [libevent >= 2.0])

AC_ARG_WITH([squareball], [AS_HELP_STRING([--with-squareball=@<:@internal/system@:>@],
            [whether to use library squareball from system [default=internal]])])
AS_IF([test "x$with_squareball" = "xsystem"], [
  SQUAREBALL="system"
  PKG_CHECK_MODULES([SQUAREBALL], [squareball >= 0.1], , [
    AC_MSG_ERROR([library squareball requested from system but not found or not new enough])
  ])
], [
  SQUAREBALL="internal"
  SQUAREBALL_CFLAGS='-I$(top_srcdir)/squareball/src'
  SQUAREBALL_LIBS='$(top_builddir)/squareball/libsquareball.la'
  AC_SUBST(SQUAREBALL_LIBS)
  AC_SUBST(SQUAREBALL_CFLAGS)
  ac_configure_args_pre="$ac_configure_args"
  ac_configure_args_post="$ac_configure_args --enable-bundleme"
  ac_configure_args="$ac_configure_args_post"
  AC_CONFIG_COMMANDS_PRE([ac_configure_args="$ac_configure_args_pre"])
  AC_CONFIG_COMMANDS_POST([ac_configure_args="$ac_configure_args_post"])
  AC_CONFIG_SUBDIRS([squareball])
  ac_configure_args="$ac_configure_args_pre"
])
AM_CONDITIONAL(INTERNAL_SQUAREBALL, [test "x$with_squareball" != "xsystem"])

AC_CONFIG_FILES([
  Makefile
  blogc-runserver.spec
])
AC_OUTPUT

AS_ECHO("
        ==== ${PACKAGE_STRING} ====

        prefix:       ${prefix}
        exec_prefix:  ${exec_prefix}
        bindir:       ${bindir}

        compiler:     ${CC}
        cflags:       ${CFLAGS}
        ldflags:      ${LDFLAGS}

        squareball:   ${SQUAREBALL}
")

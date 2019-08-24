AC_PREREQ([2.69])
AC_INIT(pyenv-doctor, 0.0.1, yamashita@geishatokyo.com)

AC_ARG_WITH([cpython], AC_HELP_STRING([--with-cpython], [check toolchain for CPython]), [WITH_CPYTHON=yes])
AC_ARG_WITH([jython], AC_HELP_STRING([--with-jython], [check toolchain for Jython]), [WITH_JYTHON=yes])
AC_ARG_WITH([pypy], AC_HELP_STRING([--with-pypy], [check toolchain for PyPy]), [WITH_PYPY=yes])
AC_ARG_WITH([stackless], AC_HELP_STRING([--with-stackless], [check toolchain for Stackless Python]), [WITH_STACKLESS=yes])

if ( test -n "$WITH_CPYTHON" || test -n "$WITH_PYPY" || test -n "$WITH_STACKLESS" ); then
  AC_PROG_CC
fi

if ( test -n "$WITH_JYTHON" ); then
  AC_CHECK_PROG(JAVA, java, java, no)
  if test "$JAVA" = "no"; then
    AC_MSG_ERROR([java is not installed.])
  fi

  AC_CHECK_PROG(ANT, ant, ant, no)
  if test "$ANT" = "no"; then
    AC_MSG_ERROR([ant is not installed.])
  fi
fi

if ( test -n "$WITH_CPYTHON" || test -n "$WITH_PYPY" || test -n "$WITH_STACKLESS" ); then
  ## GNU readline
  AC_CHECK_LIB(readline, rl_gnu_readline_p, [HAVE_LIBREADLINE=yes], [HAVE_LIBREADLINE=no])
  if test "$HAVE_LIBREADLINE" = "no"; then
    AC_MSG_ERROR([GNU readline is not installed.])
  fi
  AC_CHECK_HEADERS([readline/readline.h, readline/rlconf.h], [HAVE_READLINE_H=yes], [HAVE_READLINE_H=no], [])
  if test "$HAVE_READLINE_H" = "no"; then
    AC_MSG_ERROR([GNU readline development header is not installed.])
  fi

  ## OpenSSL
  AC_CHECK_LIB(ssl, SSL_library_init, [HAVE_LIBSSL=yes], [HAVE_LIBSSL=no])
  if test "$HAVE_LIBSSL" = "no"; then
    AC_MSG_WARN([OpenSSL <1.1 not installed. Checking v1.1 or beyond...])
    AC_CHECK_LIB(ssl, OPENSSL_init_ssl, [HAVE_LIBSSL=yes], [HAVE_LIBSSL=no])
    if test "$HAVE_LIBSSL" = "no"; then
      AC_MSG_ERROR([OpenSSL is not installed.])
    fi
  fi
  AC_CHECK_HEADERS(openssl/ssl.h, [HAVE_SSL_H=yes], [HAVE_SSL_H=no])
  if test "$HAVE_SSL_H" = "no"; then
    AC_MSG_ERROR([OpenSSL development header is not installed.])
  fi

  ## bzip2
  AC_CHECK_LIB(bz2, BZ2_bzCompressInit, [HAVE_LIBBZ2=yes], [HAVE_LIBBZ2=no])
  if test "$HAVE_LIBBZ2" = "no"; then
    AC_MSG_ERROR([bzip2 is not installed.])
  fi
  AC_CHECK_HEADERS(bzlib.h, [HAVE_BZLIB_H=yes], [HAVE_BZLIB_H=no])
  if test "$HAVE_BZLIB_H" = "no"; then
    AC_MSG_ERROR([bzip2 development header is not installed.])
  fi

  ## zlib
  AC_CHECK_LIB(z, zlibVersion, [HAVE_LIBZ=yes], [HAVE_LIBZ=no])
  if test "$HAVE_LIBZ" = "no"; then
    AC_MSG_ERROR([zlib is not installed.])
  fi
  AC_CHECK_HEADERS(zlib.h, [HAVE_ZLIB_H=yes], [HAVE_ZLIB_H=no])
  if test "$HAVE_ZLIB_H" = "no"; then
    AC_MSG_ERROR([zlib development header is not installed.])
  fi

  ## SQLite3
  AC_CHECK_LIB(sqlite3, sqlite3_initialize, [HAVE_LIBSQLITE3=yes], [HAVE_LIBSQLITE3=no])
  if test "$HAVE_LIBSQLITE3" = "no"; then
    AC_MSG_ERROR([SQLite3 is not installed.])
  fi
  AC_CHECK_HEADERS(sqlite3.h, [HAVE_SQLITE3_H=yes], [HAVE_SQLITE3_H=no])
  if test "$HAVE_SQLITE3_H" = "no"; then
    AC_MSG_ERROR([SQLite3 development header is not installed.])
  fi
fi

AC_CONFIG_FILES([Makefile])
AC_OUTPUT

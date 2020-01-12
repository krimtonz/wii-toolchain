AC_PREREQ([2.69])
AC_INIT
AC_PREFIX_DEFAULT([/opt/wii])

AC_SUBST([CFLAGS_FOR_TARGET])
AC_SUBST([CXXFLAGS_FOR_TARGET])
CFLAGS_FOR_TARGET="-g -ffunction-sections -fdata-sections -O2 $CFLAGS_FOR_TARGET"
CXXFLAGS_FOR_TARGET="-g -ffunction-sections -fdata-sections -O2 $CXXFLAGS_FOR_TARGET"
AC_SUBST([CONFIG_BINUTILS])
AC_SUBST([CONFIG_GCC])
AC_SUBST([CONFIG_NEWLIB])
AC_ARG_WITH([configure-binutils],
            [AC_HELP_STRING([--with-configure-binutils=<params>],
                            [additional parameters for binutils configuraiton])],
            [CONFIG_BINUTILS="$withval"])
AC_ARG_WITH([configure-gcc],
            [AC_HELP_STRING([--with-configure-gcc=<params>],
                            [additional parameters for gcc configuraiton])],
            [CONFIG_GCC="$withval"])
AC_ARG_WITH([configure-newlib],
            [AC_HELP_STRING([--with-configure-newlib=<params>],
                            [additional parameters for newlib configuraiton])],
            [CONFIG_NEWLIB="$withval"])

AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_MKDIR_P
AC_PROG_LN_S
AC_CHECK_PROGS([WGET], [wget curl])
AS_IF([test "x$WGET" = xwget], [WGET="wget -O"; WGET_Q="wget -q -O";],
      [test "x$WGET" = xcurl], [WGET="curl -o"; WGET_Q ="curl -s -o";])

AC_C_BIGENDIAN

AC_ARG_VAR([BINUTILS_VERSION], [select binutils version])
AC_ARG_VAR([GCC_VERSION], [select gcc version])
AC_ARG_VAR([NEWLIB_VERSION], [select newlib version])

AC_MSG_CHECKING([binutils version])
AS_IF([test -z "$BINUTILS_VERSION"],
        [
            BINUTILS_VERSION=`$WGET_Q - "https://ftp.gnu.org/gnu/binutils/" |
                              grep -E -o ">binutils-[[0-9\\\\.]]+tar\\\\.gz<" |
                              tail -n 1 |
                              sed -e s/\\>// -e s/\\\\.tar\\\\.gz\\<//`
        ])
AC_MSG_RESULT([$BINUTILS_VERSION])

AC_MSG_CHECKING([gcc version])
AS_IF([test -z "$GCC_VERSION"],
        [
            GCC_VERSION=`$WGET_Q - "https://ftp.gnu.org/gnu/gcc/" |
                              grep -E -o ">gcc-[[0-9\\\\.]]+/<" |
                              tail -n 1 |
                              sed -e s/\\>// -e s/\\\\/\\<//`
        ])
AC_MSG_RESULT([$GCC_VERSION])

AC_MSG_CHECKING([newlib version])
AS_IF([test -z "$NEWLIB_VERSION"],
        [
            NEWLIB_VERSION=`$WGET_Q - "https://sourceware.org/pub/newlib/" |
                              grep -E -o ">newlib-[[0-9\\\\.]]+tar\\\\.gz<" |
                              head -n 1 |
                              sed -e s/\\>// -e s/\\\\.tar\\\\.gz\\<//`
        ])
AC_MSG_RESULT([$NEWLIB_VERSION])
AC_CONFIG_FILES([makefile])
AC_OUTPUT
dnl Process this file with autoconf to produce a configure script.
AC_REVISION($Revision$)
AC_PREREQ(2.64)
AC_INIT(YXA, 1.0, yxa-devel@lists.su.se)
AC_CONFIG_SRCDIR([src/incomingproxy.erl])
AC_CONFIG_AUX_DIR([scripts])

AC_PROG_CC
AC_PROG_INSTALL

AC_ARG_WITH(erlang,
	AC_HELP_STRING([--with-erlang=dir],
		[search for erlang in dir]),
[if test "$withval" = "yes" -o "$withval" = "no" -o "X$with_erlang" = "X"; then
    extra_erl_path=""
else
    extra_erl_path="$with_erlang:$with_erlang/bin:"
fi
])

AC_ERLANG_NEED_ERLC([${extra_erl_path}$PATH])
AC_ERLANG_PATH_ERL([not found], [${extra_erl_path}$PATH])
AC_ERLANG_SUBST_INSTALL_LIB_DIR
AC_ERLANG_SUBST_ERTS_VER
AC_ERLANG_CHECK_LIB([kernel], , [AC_MSG_ERROR([kernel was not found!])])
AC_ERLANG_CHECK_LIB([stdlib], , [AC_MSG_ERROR([stdlib was not found!])])
AC_ERLANG_CHECK_LIB([mnesia], , [AC_MSG_ERROR([mnesia was not found!])])
AC_ERLANG_CHECK_LIB([asn1], , [AC_MSG_ERROR([asn1 was not found!])])
AC_ERLANG_CHECK_LIB([ssl], , [AC_MSG_ERROR([ssl was not found!])])
AC_ERLANG_CHECK_LIB([crypto], , [AC_MSG_ERROR([crypto was not found!])])
AC_ERLANG_CHECK_LIB([public_key], , [AC_MSG_ERROR([public_key was not found!])])
AC_ERLANG_CHECK_LIB([sasl])
AC_ERLANG_CHECK_LIB([yaws])

AC_CHECK_FILE([${ERLANG_LIB_DIR_public_key}/include/OTP-PUB-KEY.hrl],[HAS_OTP_PUB_KEY_HRL="true"],[HAS_OTP_PUB_KEY_HRL="false"])
AC_SUBST(HAS_OTP_PUB_KEY_HRL)

AC_CONFIG_FILES(
		Makefile \
		src/Makefile \
		src/config/Makefile \
		src/cpl/Makefile \
		src/event/Makefile \
		src/event_handler/Makefile \
		src/include/Makefile \
		src/local/Makefile \
		src/mysql/Makefile \
		src/eldap/Makefile \
		src/database/Makefile \
		src/transportlayer/Makefile \
		src/sipuserdb/Makefile \
		src/transactionlayer/Makefile \
		yaws/src/Makefile
	       )

AC_ARG_WITH(mnesiadir,
	AC_HELP_STRING([--with-mnesiadir=dir],
		[use dir as database for mnesia database]),
[if test "$withval" = "yes" -o "$withval" = "no" -o "X$with_mnesiadir" = "X"; then
    mnesiadir="/var/yxa/db"
else
    mnesiadir="$with_mnesiadir"
fi],[mnesiadir="/var/yxa/db"])

AC_ARG_WITH(sslcertdir,
	AC_HELP_STRING([--with-sslcertdir=dir],
		[use dir as path to your SSL certificates]),
[if test "$withval" = "yes" -o "$withval" = "no" -o "X$with_sslcertdir" = "X"; then
    sslcertdir='${confdir}'
else
    sslcertdir="$with_sslcertdir"
fi],[sslcertdir='${confdir}'])


AC_ARG_WITH(local,
	AC_HELP_STRING([--with-local=module],
		[use module as local hooks module (e.g. "my_local" - don't include the ".erl" suffix)]),
[if test "$withval" = "yes" -o "$withval" = "no" -o "X$with_local" = "X"; then
    local_module="local_default"
else
    local_module="$with_local"
fi],[local_module="local_default"])

AC_SUBST(DESTDIR)
AC_SUBST(mnesiadir)
AC_SUBST(sslcertdir)
AC_SUBST(local_module)

AC_OUTPUT


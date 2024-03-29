# Copyright (c) 2000-2007 MySQL AB, 2009 Sun Microsystems, Inc.
# Use is subject to license terms.
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU Library General Public
# License as published by the Free Software Foundation; version 2
# of the License.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Library General Public License for more details.
#
# You should have received a copy of the GNU Library General Public
# License along with this library; if not, write to the Free
# Software Foundation, Inc., 51 Franklin St, Fifth Floor, Boston,
# MA 02110-1301, USA

## Process this file with automake to create Makefile.in


if THREAD_SAFE_CLIENT
LIBMYSQLCLIENT_LA =		$(top_builddir)/libmysql_r/libmysqlclient_r.la
else
LIBMYSQLCLIENT_LA =		$(top_builddir)/libmysql/libmysqlclient.la
endif

EXTRA_DIST =		auto_increment.res auto_increment.tst \
			function.res function.tst lock_test.pl lock_test.res \
			export.pl big_record.pl \
			fork2_test.pl fork_big.pl \
			insert_and_repair.pl \
			grant.pl grant.res test_delayed_insert.pl \
			pmail.pl mail_to_db.pl table_types.pl \
			myisam-big-rows.tst \
			mysql_client_fw.c \
			CMakeLists.txt

bin_PROGRAMS =		mysql_client_test
noinst_PROGRAMS =	insert_test select_test thread_test bug25714

INCLUDES =		-I$(top_builddir)/include -I$(top_srcdir)/include \
			$(openssl_includes)
LIBS =			@CLIENT_LIBS@
LDADD =			@CLIENT_EXTRA_LDFLAGS@ \
                        $(LIBMYSQLCLIENT_LA)

mysql_client_test_LDADD= $(LDADD) $(CXXLDFLAGS)
mysql_client_test_SOURCES= mysql_client_test.c\
			$(top_srcdir)/mysys/my_memmem.c
mysql_client_test.o:	mysql_client_fw.c

insert_test_SOURCES=       insert_test.c
select_test_SOURCES=       select_test.c
insert_test_DEPENDENCIES=	$(LIBRARIES) $(pkglib_LTLIBRARIES)
select_test_DEPENDENCIES=	$(LIBRARIES) $(pkglib_LTLIBRARIES)

bug25714_SOURCES=          bug25714.c
bug25714_DEPENDENCIES=     $(LIBRARIES) $(pkglib_LTLIBRARIES)

# Fix for mit-threads
DEFS =			-DMYSQL_CLIENT_NO_THREADS

thread_test.o:		thread_test.c
			$(COMPILE) -c $(INCLUDES) $<

# Don't update the files from bitkeeper
%::SCCS/s.%

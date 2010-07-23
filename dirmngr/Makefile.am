# Makefile.am - dirmngr
# Copyright (C) 2002 Klarälvdalens Datakonsult AB
# Copyright (C) 2004, 2007, 2010 g10 Code GmbH
#
# This file is part of GnuPG.
#
# GnuPG is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3 of the License, or
# (at your option) any later version.
# 
# GnuPG is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this program; if not, see <http://www.gnu.org/licenses/>.

## Process this file with automake to produce Makefile.in

EXTRA_DIST = OAUTHORS ONEWS ChangeLog.1

bin_PROGRAMS = dirmngr dirmngr-client

libexec_PROGRAMS = dirmngr_ldap

AM_CPPFLAGS = -I$(top_srcdir)/gl -I$(top_srcdir)/intl -I$(top_srcdir)/common

include $(top_srcdir)/am/cmacros.am

AM_CFLAGS = $(LIBGCRYPT_CFLAGS) $(KSBA_CFLAGS) \
            $(LIBASSUAN_CFLAGS) $(GPG_ERROR_CFLAGS) $(PTH_CFLAGS)

BUILT_SOURCES = no-libgcrypt.c

noinst_HEADERS = dirmngr.h crlcache.h crlfetch.h misc.h

dirmngr_SOURCES = dirmngr.c dirmngr.h server.c crlcache.c crlfetch.c	\
	ldapserver.h ldapserver.c certcache.c certcache.h \
	cdb.h cdblib.c ldap.c misc.c dirmngr-err.h \
	ocsp.c ocsp.h validate.c validate.h

dirmngr_LDADD = $(libcommonpth) ../gl/libgnu.a $(DNSLIBS) $(LIBASSUAN_LIBS) \
	$(LIBGCRYPT_LIBS) $(KSBA_LIBS) $(PTH_LIBS) $(LIBINTL) $(LIBICONV)

if HAVE_W32_SYSTEM
ldap_url = ldap-url.h ldap-url.c
else
ldap_url =
endif

dirmngr_ldap_SOURCES = dirmngr_ldap.c $(ldap_url) no-libgcrypt.c
dirmngr_ldap_CFLAGS = $(GPG_ERROR_CFLAGS)
dirmngr_ldap_LDFLAGS =
dirmngr_ldap_LDADD = $(libcommon) ../gl/libgnu.a $(DNSLIBS) \
		     $(GPG_ERROR_LIBS) $(LDAPLIBS) $(LIBINTL) $(LIBICONV)

dirmngr_client_SOURCES = dirmngr-client.c no-libgcrypt.c
dirmngr_client_LDADD = $(libcommon) ../gl/libgnu.a $(LIBASSUAN_LIBS) \
	               $(GPG_ERROR_LIBS) $(LIBINTL) $(LIBICONV)


no-libgcrypt.c : $(top_srcdir)/tools/no-libgcrypt.c
	cat $(top_srcdir)/tools/no-libgcrypt.c > no-libgcrypt.c
## Autotools settings

if INTERNAL_SQUAREBALL
SUBDIRS = squareball
endif

AM_DISTCHECK_CONFIGURE_FLAGS = \
	--with-squareball=internal \
	$(NULL)

ACLOCAL_AMFLAGS = -I m4

EXTRA_DIST = \
	build-aux/git-version-gen \
	$(top_srcdir)/.version \
	autogen.sh \
	LICENSE \
	README.md \
	$(NULL)

BUILT_SOURCES = \
	$(top_srcdir)/.version \
	$(NULL)

bin_PROGRAMS = blogc-runserver

blogc_runserver_SOURCES = blogc-runserver.c

blogc_runserver_CFLAGS = \
	$(AM_CFLAGS) \
	$(LIBEVENT_CFLAGS) \
	$(SQUAREBALL_CFLAGS) \
	$(NULL)

blogc_runserver_LDADD = \
	$(LIBEVENT_LIBS) \
	$(MAGIC_LIBS) \
	$(SQUAREBALL_LIBS) \
	$(NULL)

$(top_srcdir)/.version:
	echo $(VERSION) > $@-t && mv $@-t $@

dist-hook:
	echo $(VERSION) > $(distdir)/.tarball-version

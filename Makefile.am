## Autotools settings

EXTRA_DIST = autogen.sh LICENSE README.md

bin_PROGRAMS = blogc-runserver

blogc_runserver_SOURCES = blogc-runserver.c

blogc_runserver_CFLAGS = $(LIBEVENT_CFLAGS)

blogc_runserver_LDADD = $(LIBEVENT_LIBS) $(MAGIC_LIBS)

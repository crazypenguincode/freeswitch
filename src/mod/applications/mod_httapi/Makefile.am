include $(top_srcdir)/build/modmake.rulesam
MODNAME=mod_httapi

mod_LTLIBRARIES = mod_httapi.la
mod_httapi_la_SOURCES  = mod_httapi.c
mod_httapi_la_CFLAGS   = $(AM_CFLAGS)
mod_httapi_la_LIBADD   = $(switch_builddir)/libfreeswitch.la
mod_httapi_la_LDFLAGS  = -avoid-version -module -no-undefined -shared

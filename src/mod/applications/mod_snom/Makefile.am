include $(top_srcdir)/build/modmake.rulesam
MODNAME=mod_snom

mod_LTLIBRARIES = mod_snom.la
mod_snom_la_SOURCES  = mod_snom.c
mod_snom_la_CFLAGS   = $(AM_CFLAGS)
mod_snom_la_LIBADD   = $(switch_builddir)/libfreeswitch.la
mod_snom_la_LDFLAGS  = -avoid-version -module -no-undefined -shared

include $(top_srcdir)/build/modmake.rulesam
MODNAME=mod_perl
PERL        = perl
PERL_LIBDIR =-L`perl -MConfig -e 'print $$Config{archlib}'`/CORE
PERL_LIBS   =`perl -MConfig -e 'print $$Config{libs}'`

mod_LTLIBRARIES = mod_perl.la
mod_perl_la_SOURCES  = mod_perl.c freeswitch_perl.cpp mod_perl_wrap.cpp perlxsi.c
mod_perl_la_CFLAGS   = $(AM_CFLAGS) -w
mod_perl_la_CPPFLAGS = -DMULTIPLICITY `$(PERL) -MExtUtils::Embed -e ccopts` -DEMBED_PERL -I$(switch_srcdir)/libs/stfu/ -I$(switch_srcdir)/libs/libteletone/src/ 
mod_perl_la_LIBADD   = $(switch_builddir)/libfreeswitch.la
mod_perl_la_LDFLAGS  = -avoid-version -module -no-undefined -shared `$(PERL) -MExtUtils::Embed -e ldopts` `$(PERL) -MConfig -e 'print $$Config{libs}'`

reswig:	swigclean mod_perl_wrap.cpp

swigclean: clean
	rm -f mod_perl_wrap.* freeswitch.so freeswitch.pm

mod_perl_wrap.cpp:
	swig -static -shadow -perl5 -c++ -DMULTIPLICITY -I../../../../src/include -o mod_perl_wrap.cpp freeswitch.i
	echo "#include \"mod_perl_extra.c\"" >> mod_perl_wrap.cpp
	patch -s -p0 -i hack.diff

orig: mod_perl_wrap.cpp
	patch -R -s -p0 -i hack.diff

freeswitch.$(LIBTOOL_LIB_EXTEN): $(LOCAL_OBJS) $(LOCAL_LIBADD)
	$(CXXLINK) $(SOLINK) -o freeswitch.$(LIBTOOL_LIB_EXTEN) $(LOCAL_OBJS) $(LOCAL_LIBADD) $(LDFLAGS)

BUILT_SOURCE=freeswitch.$(LIBTOOL_LIB_EXTEN)

.perlok:
	@(${PERL} -V | grep -i usemultiplicity=define >/dev/null && echo Phew, You have the right perl.) \
	|| ((echo Sorry, you need to compile perl with threads and multiplicity.&& exit 1))
	@touch .perlok

clean:
	rm -fr *~ .perlok .libs freeswitch.$(LIBTOOL_LIB_EXTEN) 2>/dev/null

install:
	mkdir -p $(DESTDIR)$(prefix)/perl
	$(LTINSTALL) freeswitch.$(LIBTOOL_LIB_EXTEN) freeswitch.pm $(DESTDIR)$(prefix)/perl
	if [ ! -f $(DESTDIR)$(prefix)/perl/freeswitch.pm ] ; then $(LTINSTALL) freeswitch.pm $(DESTDIR)$(prefix)/perl ; fi

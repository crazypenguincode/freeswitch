include $(top_srcdir)/build/modmake.rulesam
MODNAME=mod_rayo

IKS_DIR=$(switch_srcdir)/libs/iksemel
PCRE_DIR=$(switch_srcdir)/libs/pcre
IKS_LA=$(IKS_DIR)/src/libiksemel.la
PCRE_LA=$(PCRE_DIR)/libpcre.la

mod_LTLIBRARIES = mod_rayo.la
mod_rayo_la_SOURCES  = mod_rayo.c iks_helpers.c nlsml.c rayo_components.c rayo_cpa_component.c rayo_cpa_detector.c rayo_elements.c rayo_fax_components.c
mod_rayo_la_SOURCES += rayo_input_component.c rayo_output_component.c rayo_prompt_component.c rayo_record_component.c sasl.c srgs.c xmpp_streams.c
mod_rayo_la_CFLAGS   = $(AM_CFLAGS) -I$(switch_srcdir)/libs/iksemel/include -I$(switch_srcdir)/libs/pcre
mod_rayo_la_LIBADD   = $(switch_builddir)/libfreeswitch.la $(IKS_LA) $(PCRE_LA) 
mod_rayo_la_LDFLAGS  = -avoid-version -module -no-undefined -shared

BUILT_SOURCES=$(IKS_LA) $(PCRE_LA)

$(IKS_LA): $(IKS_DIR) $(IKS_DIR)/.update
	@cd $(IKS_DIR) && $(MAKE)
	@$(TOUCH_TARGET)

$(PCRE_LA): $(PCRE_DIR) $(PCRE_DIR)/.update
	@cd $(PCRE_DIR) && $(MAKE)
	@$(TOUCH_TARGET)

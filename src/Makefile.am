
vmoddir = $(VMOD_DIR)
vmod_LTLIBRARIES = libvmod_throttle.la

libvmod_throttle_la_CFLAGS = $(VMOD_INCLUDES)
libvmod_throttle_la_LDFLAGS = -module -export-dynamic -avoid-version -shared \
	$(LIBS)

libvmod_throttle_la_SOURCES = \
	vmod_throttle.c
nodist_libvmod_throttle_la_SOURCES = \
	vcc_if.c \
	vcc_if.h

dist_man_MANS = vmod_throttle.3

VMOD_TESTS = tests/*.vtc

$(libvmod_throttle_la_OBJECTS): vcc_if.h

vcc_if.c vcc_if.h vmod_throttle.man.rst: $(VMODTOOL) $(top_srcdir)/src/vmod_throttle.vcc
	$(PYTHON) $(VMODTOOL) $(top_srcdir)/src/vmod_throttle.vcc

vmod_throttle.3: vmod_throttle.man.rst
	${RST2MAN} $? $@

check:
	$(VARNISHTEST) -Dvarnishd=$(VARNISHD) \
	    -Dvmod_topbuild=$(abs_top_builddir) $(VMOD_TESTS)

EXTRA_DIST = vmod_throttle.vcc \
	$(VMOD_TESTS)

CLEANFILES = $(builddir)/vcc_if.c \
	$(builddir)/vcc_if.h \
	$(builddir)/vmod_throttle.man.rst \
	$(builddir)/vmod_throttle.rst \
	$(builddir)/$(dist_man_MANS)

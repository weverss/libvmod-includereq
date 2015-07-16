AM_CPPFLAGS = @VMOD_INCLUDES@ -Wall -Werror

vmoddir = @VMOD_DIR@
vmod_LTLIBRARIES = libvmod_includereq.la

libvmod_includereq_la_LDFLAGS = -module -export-dynamic -avoid-version -shared

libvmod_includereq_la_SOURCES = \
	vmod_includereq.c

nodist_libvmod_includereq_la_SOURCES = \
	vcc_if.c \
	vcc_if.h

vmod_includereq.lo: vcc_if.c vcc_if.h

vcc_if.c: vcc_if.h

vcc_if.h: @VMODTOOL@ $(top_srcdir)/src/vmod_includereq.vcc
	@VMODTOOL@ $(top_srcdir)/src/vmod_includereq.vcc

VMOD_TESTS = $(top_srcdir)/src/tests/*.vtc
.PHONY: $(VMOD_TESTS)

$(top_srcdir)/src/tests/*.vtc: libvmod_includereq.la
	@VARNISHTEST@ -Dvarnishd=@VARNISHD@ -Dvmod_topbuild=$(abs_top_builddir) $@

check: $(VMOD_TESTS)

EXTRA_DIST = \
	vmod_includereq.vcc \
	$(VMOD_TESTS)

CLEANFILES = \
	$(builddir)/vcc_if.c \
	$(builddir)/vcc_if.h \
	$(builddir)/vmod_includereq.rst \
	$(builddir)/vmod_includereq.man.rst

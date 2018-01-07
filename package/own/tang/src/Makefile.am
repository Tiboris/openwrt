AM_CFLAGS = @TANG_CFLAGS@ @jose_CFLAGS@
LDADD = @jose_LIBS@ @http_parser_LIBS@

nagiosdir = $(libdir)/nagios/plugins
cachedir = $(localstatedir)/cache/$(PACKAGE_NAME)
jwkdir = $(localstatedir)/db/$(PACKAGE_NAME)

dist_libexec_SCRIPTS = src/tangd-update src/tangd-keygen
libexec_PROGRAMS = src/tangd
man8_MANS = doc/tang.8

src_tangd_SOURCES = src/http.c src/http.h src/tangd.c

%: %.in
	$(AM_V_GEN)mkdir -p "`dirname "$@"`"
	$(AM_V_GEN)$(SED) \
		-e 's,@libexecdir\@,$(libexecdir),g' \
		-e 's,@jwkdir\@,$(jwkdir),g' \
		-e 's,@cachedir\@,$(cachedir),g' \
		$(srcdir)/$@.in > $@

AM_TESTS_ENVIRONMENT = SD_ACTIVATE="@SD_ACTIVATE@" PATH=$(srcdir)/src:$(builddir)/src:$(PATH)
TESTS = tests/adv tests/rec 

EXTRA_DIST = \
    COPYING \
    $(TESTS) \
    $(man1_MANS) \
    $(man8_MANS)

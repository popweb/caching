NAME := varnish
VERSION := 3.0.3
SPEC_FILE := $(NAME).spec
TARBALL := $(NAME)-$(VERSION).tar.gz
SRCDIR ?= ./
DESTDIR ?= ./

.PHONY: srpm

srpm: $(TARBALL) $(SPEC_FILE)
	rpmbuild --define '_sourcedir $(SRCDIR)' --define '_srcrpmdir $(DESTDIR)' -bs $(SPEC_FILE) | tee $(DESTDIR)/srpm.list

$(TARBALL): $(NAME)-$(VERSION)
	tar zcf $@ $^

clean:
	rm -fv *gz *rpm

build: srpm
	rpmbuild --rebuild `grep -ow $(DESTDIR).*src.rpm $(DESTDIR)/srpm.list`

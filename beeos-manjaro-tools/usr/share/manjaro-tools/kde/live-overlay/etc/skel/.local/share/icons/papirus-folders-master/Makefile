PREFIX ?= /usr
PROGNAME := papirus-folders
VERSION ?=

all:

install:
	mkdir -p $(DESTDIR)$(PREFIX)/bin
	install -m 755 $(PROGNAME) $(DESTDIR)$(PREFIX)/bin
	mkdir -p $(DESTDIR)$(PREFIX)/share/bash-completion/completions
	install -m 644 completion/$(PROGNAME) \
		$(DESTDIR)$(PREFIX)/share/bash-completion/completions
	mkdir -p $(DESTDIR)$(PREFIX)/share/zsh/vendor-completions
	install -m 644 completion/_$(PROGNAME) \
		$(DESTDIR)$(PREFIX)/share/zsh/vendor-completions

uninstall:
	rm -f $(DESTDIR)$(PREFIX)/bin/$(PROGNAME)
	rm -f $(DESTDIR)$(PREFIX)/share/bash-completion/completions/$(PROGNAME)
	rm -f $(DESTDIR)$(PREFIX)/share/zsh/vendor-completions/_$(PROGNAME)

_get_version:
ifndef VERSION
	$(error VERSION is not defined. Pass via "make bump VERSION=0.1.2")
endif

bump: _get_version
	sed -i '/VERSION=/s/[0-9.]\+/$(VERSION)/' $(PROGNAME)
	dch -v $(VERSION)-1 -- ''
	git commit -am "Bump to v$(VERSION)"
	git tag -f v$(VERSION)

release:
	git push origin
	git push origin --tags


.PHONY: all install uninstall _get_version bump release
